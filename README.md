### Mục tiêu: 
- Hiểu mối quan hệ giữa Kubernetes và container.  
- Tìm hiểu kiến trúc Kubernetes, bao gồm các thành phần master và node.  
- Thành thạo việc triển khai ứng dụng bằng pod và container.  
- Khám phá hệ thống mạng và dịch vụ của Kubernetes.  
- Nắm vững việc quản lý các khối lưu trữ và dung lượng lưu trữ trong môi trường Kubernetes.

## **Mô-đun 1: Kubernetes Fundamentals và Triển khai Kubernetes**  
- Bài học mở đầu  
- Các nguyên lý cơ bản của Kubernetes  
- Triển khai và các thành phần trong Kubernetes

### **I. Tóm tắt nội dung về Kubernetes và mối quan hệ với container:**  

1. **Nguồn gốc của Kubernetes:**  
   - Tên "Kubernetes" bắt nguồn từ tiếng Hy Lạp, có nghĩa là người lái tàu hoặc hoa tiêu.  
   - Được phát triển bởi các kỹ sư của Google gồm Ville Aikas, Joe Beda, Brendan Burns và Craig McLuckie, công bố lần đầu vào giữa năm 2014.  
   - Thiết kế và phát triển của Kubernetes chịu ảnh hưởng lớn từ hệ thống nội bộ Bark của Google. Ban đầu, dự án có tên mã là "Project 7", liên quan đến nhân vật "Seven of Nine" trong Star Trek, và logo của Kubernetes có 7 nan hoa đại diện cho tên mã này.  
   - Kubernetes còn được gọi là **K8s**, vì giữa chữ K và S có 8 ký tự.

2. **Tại sao cần Kubernetes khi đã có container như Docker?**  
   - Kubernetes giải quyết các vấn đề mà container không tự xử lý được, như:
     - Giám sát container và đảm bảo tính sẵn sàng khi một container gặp sự cố.  
     - Cung cấp khả năng chịu lỗi, tính sẵn sàng cao, và đảm bảo độ tin cậy.  
     - Tự động xử lý khi có sự cố xảy ra trên hệ điều hành hoặc máy chủ vật lý/ảo.

3. **Quản lý container trong môi trường thực tế:**  
   - Trong môi trường sản xuất, thường có nhiều container chạy đồng thời. Kubernetes hỗ trợ việc:
     - Kết nối các container với nhau và với hệ thống backend.  
     - Điều chỉnh số lượng container khi tải ứng dụng tăng lên.  
     - Tối ưu hóa quản lý mạng và kết nối giữa các container.  
   
4. **Tính năng mở rộng và linh hoạt:**  
   - Kubernetes là công nghệ mã nguồn mở, hiện được duy trì bởi **Cloud Native Computing Foundation (CNCF)**.  
   - Nó hỗ trợ mở rộng tính năng và có thể triển khai trên các nền tảng như **PaaS**, **IaaS**, hoặc **on-premises** và cloud.  
   - Dù triển khai trên bất kỳ nền tảng nào, Kubernetes vẫn đảm bảo khả năng quản lý nhất quán.

5. **Đặc điểm nổi bật:**  
   - **Quản lý tình trạng tài nguyên:** Kubernetes liên tục kiểm tra trạng thái của các thành phần được triển khai, đảm bảo chúng luôn hoạt động tốt.  
   - **Tự động hóa và autoscaling:** Kubernetes tự động tăng hoặc giảm số lượng tài nguyên khi cần thiết để đáp ứng nhu cầu tải của ứng dụng.  

=> Tóm lại, Kubernetes là một công cụ mạnh mẽ giúp quản lý môi trường container hóa, cung cấp khả năng mở rộng, tự động hóa và đảm bảo tính sẵn sàng cao trong các hệ thống sản xuất phức tạp.

### **II. Tóm tắt kiến trúc Kubernetes:**  

![image](https://github.com/user-attachments/assets/61400d7d-1614-4831-b047-c049e385ecf1)


1. **Kubernetes Master và Node:**  
   - **Kubernetes Master** là thành phần quan trọng nhất, quản lý toàn bộ cụm (cluster) và các **node** – nơi container thực sự chạy.  
   - Master có thể triển khai trên một hoặc nhiều máy chủ và hỗ trợ cấu hình **multi-master** để đảm bảo khả năng mở rộng và độ tin cậy cao.  
   - Các **node** là các máy tính vật lý hoặc máy ảo, có thể mở rộng từ một đến hàng trăm máy, và Master sẽ thêm chúng vào cụm để quản lý.  

2. **Mô hình Client-Server:**  
   - Kubernetes hoạt động theo mô hình **client-server**, trong đó Master đóng vai trò như server và các node đóng vai trò như client.  

3. **Pod – Đơn vị nhỏ nhất trong Kubernetes:**  
   - Kubernetes không chạy trực tiếp container mà sử dụng **pod** – đơn vị nhỏ nhất có thể chứa một hoặc nhiều container.  
   - Các container trong cùng một pod dùng chung tài nguyên như **mạng** (IP riêng cho mỗi pod) và **lưu trữ** (shared storage).  
   - Việc sử dụng pod giúp tăng hiệu quả giao tiếp giữa các container và quản lý tài nguyên dễ dàng hơn.  

4. **Control Plane:**  
   - **Control Plane** (hay Kubernetes Master) giám sát các node và điều khiển việc triển khai pod trên chúng.  
   - Control Plane có thể chạy trên nhiều máy khác nhau, giúp tăng khả năng chịu lỗi và duy trì hệ thống khi một node gặp sự cố.  
   - Nếu một node bị lỗi, Kubernetes sẽ tự động tái triển khai pod trên các node còn lại. Tuy nhiên, nếu **Master** gặp sự cố, toàn bộ hệ thống sẽ dừng hoạt động vì Master là thành phần trung tâm.  

5. **Khả năng chịu lỗi và mở rộng:**  
   - Hệ thống có khả năng tự động phát hiện lỗi, tái triển khai pod và mở rộng tài nguyên bằng cách thêm nhiều node vào cụm khi cần thiết.  
   - Control Plane đảm bảo tính **khả dụng cao** và khả năng **tự phục hồi** khi có lỗi xảy ra trong các node.  

**Mô-đun 2: Kubernetes Pods, Deployments, Replica Sets, Networking và Storage**  
- Cấu hình và quản lý Kubernetes  
- Quản lý mạng, dịch vụ và lưu trữ trong Kubernetes  
