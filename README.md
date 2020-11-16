# Docker và những kiến thức cơ bản 
## Docker là gì?
Docker là công cụ tạo môi trường được "đóng gói" (container)  trên máy tính. nó không làm tác động tới môi trường hiện tại của máy.
Nó cho phép bạn đóng gói, triển khai và chạy các ứng dụng một cách nhanh chóng. 
* Nó giống như virtual machine, chỉ là tiện dụng hơn, dễ dàng sử dụng hơn và độc lập với hệ điều hành máy chủ chúng ta đang sử dụng.
* Khi sử dụng môi trường *Vitualization* thì chúng ta cần cài các hệ điều hành cùng cái tool cần thiết để chạy ứng dụng có sẵn, nhưng với docker thì việc đó trở nên đơn giản với việc mình tìm và sử dụng các image (môi trường được dev tạo sẵn rồi upload lên). Sau đó đóng gói trong các *Container* và chạy thôi.
## Tại sao Cchusng ta nên sử dụng Docker ?
* Tính không thay đổi: Một Immutablity image chứa mọi thứ để chạy một ứng dụng bao gồm cả source code của mình.
* Có thể tái sử dụng dễ dàng.
* Bạn có thể chia sẻ cho bất cứ ai muốn chạy ứng dụng của mình, chỉ cần sử dụng các image có sẵn mà Bạn đang sử dụng vật là chúng ta đã có một *same enviroment* .
    * **Ví dụ**: Bạn của mình đang làm project với Nodejs và nó đang nhờ mình test hộ nó trên máy của mình mà project của nó vẫn chưa up lên host, có nghĩa là vẫn ở local. Tuy nhiên mình chưa bao giờ lập trình với Nodejs nên không biết các tool cần thiết để chạy ứng dụng.
    * Vấn đề đề trên đã được giải quyết với *docker*. Việc mình cần làm chỉ là hỏi  cần cài những tool và version nào . sau đó lên google tìm các image cần thiết để chứa môi trường mình cần chạy và chạy thôi.
* **Automation**: Tính tự động, khác dễ dàng đễ start server chỉ thông qua vài dòng lệnh trên terminal
* **Versioning**: Có thể dễ dàng chọn các phiên bản của ứng dụng cần thiết (ví dụ như mysql5.7, laravel5 ...) vì hầu hết cộng đồng docker update khác nhanh chóng.
* **Tính độc lập**:  Mình không cài trực tiếp các ứng dụng server cần thiết cho app của mình lên máy một các locally mà các cài đặt cần thiết được build trong các gói (image).

## Các khái niệm cần thiết
### Image
Hiểu đơn giản nó sẽ chứa các cài đặt sẵn để cho chúng ta sử dụng. Nó như cái hộp bọc lấy phần setup của mình.
* Ví dụ mình cần cài apache2 thì mình sẽ chạy câu lênh cần thiết để cài đặt nó, tuy nhiên nếu mình sử dụng docker thì mình chỉ cần lên mạng tìm image nào chứa apache2 mà dùng thôi, mọi gói và setup cần thiết đã được đặt trong image
### Container
Nó là các instance của các image mà mình có. Chúng ta có các image về service cần thiết rồi, việc cần làm là run các thằng image đó vào trong các container và dùng thằng nào thì start thằng đó.
### Volume
Volume là cách dễ dàng để chia sẻ vùng nhớ giữa máy chủ của mình và container. Nó được tạo ra trong suốt quá trình container được chạy và luôn được đồng bộ
### Expose port(Cổng ứng dụng)
* Ví dụ mình dùng mysql container, bên ngoài mình cài mysql-workbench để làm việc, mặc định bên trong container sẽ setup cổng đối với mysql là 3306 đúng không, nhưng nếu mà bên ngoài máy local của mình đã sử dụng port 3306 cho mục đích nào đó => Conflict. Và mình sẽ không thể dùng workbench tạo connection tới port 3306 được.
* Làm việc với docker mình có thể export cổng bên trong container ra cổng bên ngoài tương ứng. Ví dụ trong conatainer port 3306 của mysql thì mình sẽ export nó ra bên ngoài là 3307 chẳng hạn => Vấn đề được giải quyết