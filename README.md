[Link bài học](https://www.coursera.org/learn/certified-kubernetes-application-developer-kubernetes-fundamentals/lecture/CfLd4/kubernetes-networking-architecture-container-to-container-pod-to-pod-pod-to)
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

### **1. Tóm tắt nội dung về Kubernetes và mối quan hệ với container:**  

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

### **2. Tóm tắt kiến trúc Kubernetes:**  

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

### **2. Kubernetes Master Components:**  

1. **ETCD**: Là một kho dữ liệu kiểu key-value có độ sẵn sàng cao, nơi lưu trữ tất cả dữ liệu của cụm Kubernetes, như cấu hình và trạng thái. Việc sao lưu ETCD là rất quan trọng để đảm bảo khôi phục khi gặp sự cố. ETCD được mã hóa và có thể sử dụng độc lập với Kubernetes.

2. **API Server (kube-apiserver)**: API Server là thành phần duy nhất giao tiếp trực tiếp với ETCD. Nó đóng vai trò là cổng giao tiếp cho các tương tác với cụm Kubernetes, xử lý các yêu cầu API như tạo, xóa hoặc mở rộng các pod. Nó cũng quản lý xác thực, ủy quyền và phân phối lưu lượng thông qua việc mở rộng theo chiều ngang, cho phép nhiều phiên bản xử lý lưu lượng. API Server giao tiếp với cơ sở dữ liệu ETCD để thực hiện các hành động theo yêu cầu.

3. **Controller Manager**: Đây là một dịch vụ chạy trên nút master, chịu trách nhiệm quản lý các controller khác nhau như:
   - **Node Controller**: Xử lý khi các nút gặp sự cố.
   - **Job Controller**: Tạo và quản lý các pod cho các tác vụ cụ thể.
   - **Endpoint Controller**: Kết nối các dịch vụ với các pod.
   - **Service Account và Token Controller**: Quản lý việc tạo tài khoản và mã thông báo API cho các namespace.
   - Controller Manager cũng xử lý việc thu gom rác, bao gồm vòng đời của các sự kiện và tài nguyên trong cụm.

4. **Scheduler (kube-scheduler)**: Scheduler chịu trách nhiệm phân công các pod mới được tạo cho các nút có sẵn, dựa trên yêu cầu về tài nguyên, chính sách và các ràng buộc. Nó đảm bảo rằng các pod được phân bổ vào các nút thích hợp với đủ tài nguyên, xử lý các tình huống như dung lượng bộ nhớ hoặc các ràng buộc về affinity.

### **3. Kubernetes Node Components:**  

1. **Kubelet**: Là một agent chạy trong mỗi node, có nhiệm vụ đảm bảo rằng các container trong pod hoạt động đúng và khỏe mạnh. Kubelet lấy thông tin về pod từ API Server và duy trì các container. Kubelet chỉ quản lý các container được tạo ra bởi Kubernetes, không phải những container được tạo trực tiếp trong node.

2. **Kube Proxy**: Là một proxy mạng chạy trên mỗi node. Nó duy trì các quy tắc mạng cho phép giao tiếp giữa các pod trong cùng một node hoặc giữa các node khác. Kube Proxy cũng theo dõi sự thay đổi của các pod và cập nhật các quy tắc mạng khi có sự thay đổi.

3. **Container Runtime**: Là phần mềm chịu trách nhiệm chạy container. Kubernetes hỗ trợ nhiều container runtimes như Docker, ContainerD, và CRI-O, cho phép người dùng chọn lựa. Mục đích của container runtime là cung cấp môi trường chạy container, trong khi Kubernetes đảm nhận các nhiệm vụ khác như quản lý và duy trì hệ thống.

4. **cAdvisor**: Là một dịch vụ do Google phát triển, cung cấp thông tin về việc sử dụng tài nguyên và hiệu suất của các container đang chạy. Nó theo dõi các container, thu thập dữ liệu về mức độ sử dụng tài nguyên, và xuất dữ liệu này ra ngoài để Kubernetes có thể theo dõi tình trạng của các container.

### **4. Deployment Using Pod or Container:**  

1. **Tạo Pod**: Ứng dụng của bạn sẽ được đóng gói trong một container, và sau đó được triển khai vào một **Pod**. Mỗi Pod có thể chứa một hoặc nhiều container.
   
2. **Chạy trên Node**: Pod sẽ chạy trên một **node** (có thể là máy ảo hoặc máy vật lý). Các node này không phải là thành phần của Kubernetes master, nhưng chúng được quản lý bởi **control plane**. Control plane giám sát tình trạng của các pod và đảm bảo các pod chạy ổn định trên node.

3. **Quản lý Pod và Container**: **Kubelet** giúp giao tiếp giữa **control plane** và **node**, và quản lý các pod cũng như container chạy trên máy chủ.

4. **Container Runtime**: Chịu trách nhiệm kéo image container từ registry (ví dụ: Docker Hub hoặc registry riêng của bạn), sau đó thực hiện các tác vụ như giải nén, chạy container và xử lý mạng cấp thấp.

5. **Triển khai với Deployment**: Nếu bạn muốn triển khai nhiều bản sao của một Pod, bạn có thể sử dụng **Deployment**. Deployment là đối tượng trong Kubernetes cho phép bạn xác định số lượng Pod cần chạy, cơ chế cân bằng tải và khả năng tự động điều chỉnh (auto-scaling).

6. **Quản lý cập nhật**: Deployment cũng giúp bạn quản lý việc cập nhật ứng dụng, với các cơ chế như **upgrade in place** hoặc **rolling update**, giúp quá trình cập nhật diễn ra mượt mà mà không làm gián đoạn dịch vụ.

### **5. VirtualBox:**

1. **Khái niệm về Máy Ảo**:
   - **Máy ảo** (VM) là một giải pháp ảo hóa cho phép bạn chạy nhiều hệ điều hành trên một máy vật lý. Thay vì cài đặt nhiều hệ điều hành (Windows và Linux) và chọn giữa chúng khi khởi động, máy ảo cho phép bạn chạy một hệ điều hành con (guest OS) trên hệ điều hành chủ (host OS) mà không cần khởi động lại máy.

2. **VirtualBox**:
   - **VirtualBox** là phần mềm mã nguồn mở giúp bạn tạo và chạy máy ảo trên các hệ điều hành như Windows, Linux, hoặc Mac.
   - Bạn có thể chạy nhiều máy ảo trong VirtualBox tùy thuộc vào dung lượng bộ nhớ và sức mạnh CPU của máy chủ (host machine). Ví dụ, nếu laptop của bạn có 16GB RAM, bạn có thể chạy nhiều máy ảo cùng lúc.

3. **Quy trình sử dụng VirtualBox**:
   - **Cài đặt**: Sau khi cài đặt VirtualBox trên hệ điều hành chủ (Windows 10), bạn có thể tải về và cài đặt hệ điều hành con (ví dụ: Ubuntu Linux) từ ISO image.
   - **Máy chủ và máy khách**: Hệ điều hành chủ là Windows, còn hệ điều hành con (Linux) sẽ chạy trong VirtualBox như một máy khách.
   - **Môi trường kiểm thử**: Bạn có thể phát triển và kiểm thử ứng dụng trên hệ điều hành chủ và hệ điều hành con mà không cần phải sử dụng máy tính khác.

4. **Lợi ích của VirtualBox**:
   - **Tiết kiệm chi phí và không gian**: Bạn không cần phần cứng riêng cho mỗi hệ điều hành, giúp tiết kiệm chi phí và không gian.
   - **Môi trường cách ly**: VirtualBox hoạt động như một môi trường sandbox, mọi thứ diễn ra trong không gian đó và không ảnh hưởng đến hệ điều hành chủ.
   - **Kiểm thử nhanh**: Bạn có thể dễ dàng kiểm thử phần mềm trên nhiều hệ điều hành mà không cần chuyển đổi giữa các máy tính hoặc cài đặt lại.
   - **Bảo mật và an toàn**: VirtualBox cho phép bạn cài đặt phần mềm mà không lo làm hỏng hệ điều hành chủ.

5. **Nhược điểm**:
   - **Giảm hiệu suất**: VirtualBox chiếm dụng bộ nhớ và CPU của hệ điều hành chủ, điều này có thể làm chậm hệ thống nếu bạn chạy quá nhiều máy ảo hoặc phân bổ quá nhiều tài nguyên cho các máy ảo.
   - **Tài nguyên hệ thống bị chia sẻ**: Khi chạy máy ảo, bạn phải phân bổ một phần bộ nhớ và CPU cho máy ảo, khiến hệ điều hành chủ còn lại ít tài nguyên hơn.

### **6. Danh sách các lệnh Kubernetes (K8s):**

1. **kubectl get**  
   - **Cú pháp**: `kubectl get [resource] [flags]`
   - **Tùy chọn**:
     - `-o, --output`: Xác định định dạng đầu ra (json|yaml|wide|custom-columns=...).
     - `--all-namespaces`: Hiển thị tài nguyên từ tất cả các không gian tên.
   - **Giải thích**: Lấy thông tin về một hoặc nhiều tài nguyên Kubernetes.
   - **Ví dụ**: `kubectl get pods --all-namespaces`

2. **kubectl describe**  
   - **Cú pháp**: `kubectl describe [resource] [name] [flags]`
   - **Tùy chọn**:
     - `--all-namespaces`: Hiển thị tài nguyên từ tất cả các không gian tên.
   - **Giải thích**: Cung cấp thông tin chi tiết về một tài nguyên Kubernetes cụ thể.
   - **Ví dụ**: `kubectl describe pod my-pod`

3. **kubectl create**  
   - **Cú pháp**: `kubectl create -f <filename> [flags]`
   - **Tùy chọn**:
     - `-f, --filename`: Xác định tệp tin, thư mục hoặc URL để tạo tài nguyên.
   - **Giải thích**: Tạo tài nguyên Kubernetes mới từ tệp tin hoặc URL.
   - **Ví dụ**: `kubectl create -f pod.yaml`

4. **kubectl apply**  
   - **Cú pháp**: `kubectl apply -f <filename> [flags]`
   - **Tùy chọn**:
     - `-f, --filename`: Xác định tệp tin, thư mục hoặc URL để áp dụng tài nguyên.
   - **Giải thích**: Tạo hoặc cập nhật tài nguyên Kubernetes dựa trên cấu hình đã cung cấp.
   - **Ví dụ**: `kubectl apply -f deployment.yaml`

5. **kubectl delete**  
   - **Cú pháp**: `kubectl delete [resource] [name] [flags]`
   - **Tùy chọn**:
     - `--all`: Xóa tất cả tài nguyên của các loại được chỉ định.
   - **Giải thích**: Xóa một hoặc nhiều tài nguyên Kubernetes.
   - **Ví dụ**: `kubectl delete pod my-pod`

6. **kubectl logs**  
   - **Cú pháp**: `kubectl logs [pod-name] [flags]`
   - **Tùy chọn**:
     - `-f, --follow`: Tiếp tục phát trực tiếp các nhật ký.
   - **Giải thích**: Lấy nhật ký của một pod cụ thể.
   - **Ví dụ**: `kubectl logs my-pod`

7. **kubectl exec**  
   - **Cú pháp**: `kubectl exec [pod-name] [command] [flags]`
   - **Tùy chọn**:
     - `-it, --stdin`: Giữ stdin mở trên các container trong pod.
   - **Giải thích**: Thực thi lệnh trong một container đang chạy.
   - **Ví dụ**: `kubectl exec -it my-pod -- /bin/bash`

8. **kubectl scale**  
   - **Cú pháp**: `kubectl scale [resource] [name] --replicas=[count] [flags]`
   - **Giải thích**: Điều chỉnh số lượng bản sao cho một deployment, replicaset, hoặc statefulset.
   - **Ví dụ**: `kubectl scale deployment my-deployment --replicas=3`

9. **kubectl rollout**  
   - **Cú pháp**: `kubectl rollout [resource] [name] [flags]`
   - **Giải thích**: Quản lý các bản cập nhật cuộn cho các deployment.
   - **Ví dụ**: `kubectl rollout status deployment my-deployment`

10. **kubectl port-forward**  
    - **Cú pháp**: `kubectl port-forward [pod-name] [local-port]:[pod-port] [flags]`
    - **Giải thích**: Chuyển tiếp các cổng máy tính cục bộ đến một cổng trên pod.
    - **Ví dụ**: `kubectl port-forward my-pod 8080:80`

### **7. Kubernetes Case Studies:**

1. **Spotify**:
   - **Vấn đề**: Spotify, dịch vụ phát nhạc trực tuyến phổ biến, đã áp dụng Kubernetes để quản lý cơ sở hạ tầng microservices của mình.
   - **Lợi ích**:
     - Kubernetes giúp Spotify đạt được thời gian triển khai nhanh hơn, cải thiện khả năng mở rộng và tối ưu hóa sử dụng tài nguyên.
     - Nhờ Kubernetes, các nhóm kỹ sư của Spotify có thể tập trung nhiều hơn vào việc phát triển tính năng và ít phải lo lắng về việc quản lý cơ sở hạ tầng.

2. **Grab**:
   - **Vấn đề**: Grab, công ty hàng đầu trong lĩnh vực gọi xe và logistics tại Đông Nam Á, sử dụng Kubernetes để vận hành nền tảng của mình.
   - **Lợi ích**:
     - Kubernetes giúp Grab triển khai và mở rộng các dịch vụ nhanh chóng, xử lý tải giao thông cao hiệu quả và duy trì khả năng sẵn sàng cao.
     - Với Kubernetes, Grab có thể cung cấp các tính năng và dịch vụ mới cho người dùng nhanh chóng đồng thời đảm bảo tính ổn định và tin cậy.

3. **Airbnb**:
   - **Vấn đề**: Airbnb, nền tảng giao dịch trực tuyến cho thuê chỗ ở và các trải nghiệm du lịch, sử dụng Kubernetes để quản lý các ứng dụng container của mình.
   - **Lợi ích**:
     - Kubernetes cung cấp cho Airbnb một nền tảng mở rộng và đáng tin cậy để triển khai và điều phối kiến trúc microservices.
     - Việc sử dụng Kubernetes đã cải thiện tốc độ phát triển, giảm chi phí hạ tầng và nâng cao độ tin cậy tổng thể của nền tảng.

4. **Pinterest**:
   - **Vấn đề**: Pinterest, nền tảng khám phá và lưu trữ hình ảnh, sử dụng Kubernetes để tinh giản quy trình phát triển và triển khai.
   - **Lợi ích**:
     - Kubernetes giúp Pinterest triển khai các bản cập nhật dịch vụ một cách mượt mà, mở rộng tài nguyên linh hoạt theo nhu cầu và đạt được khả năng sẵn sàng cao.
     - Với Kubernetes, các nhóm kỹ sư của Pinterest có thể lặp lại nhanh chóng, thử nghiệm các tính năng mới và mang lại trải nghiệm tốt hơn cho người dùng.

5. **The New York Times**:
   - **Vấn đề**: The New York Times, tờ báo hàng đầu, đã di chuyển cơ sở hạ tầng của mình lên Kubernetes để hiện đại hóa nền tảng và cải thiện hiệu quả hoạt động.
   - **Lợi ích**:
     - Kubernetes giúp The New York Times tự động hóa các quy trình triển khai, tối ưu hóa việc sử dụng tài nguyên và mở rộng dịch vụ một cách linh hoạt.
     - Bằng cách áp dụng Kubernetes, The New York Times có thể cung cấp nội dung tin tức cho độc giả một cách đáng tin cậy và hiệu quả hơn, đồng thời giảm chi phí hạ tầng.

## Mô-đun 2: Kubernetes Pods, Deployments, Replica Sets, Networking và Storage
- Cấu hình và quản lý Kubernetes  
- Quản lý mạng, dịch vụ và lưu trữ trong Kubernetes  

### **1. Kubernetes và Cách Tiếp Cận Cấu Hình**:

Trong Kubernetes, chúng ta có thể triển khai ứng dụng bằng cách sử dụng YAML để cung cấp các chỉ dẫn cấu hình hoặc sử dụng cách tiếp cận theo lệnh (imperative approach). Cách tiếp cận theo lệnh là phương pháp sử dụng dòng lệnh. Khi bạn sử dụng `kubectl`, đó là công cụ dòng lệnh mà Kubernetes cung cấp, cho phép bạn kết nối với bất kỳ cụm Kubernetes nào từ máy tính của bạn và thực hiện các thao tác như tạo, cập nhật hoặc xóa các tài nguyên trong Kubernetes.

1. **Tạo Pod**: Để chạy một pod, bạn sử dụng lệnh:
   ```bash
   kubectl run <tên-pod>
   ```
   Đây là cách đơn giản để tạo một pod, như chúng ta đã thấy trong demo trước với Minikube.

2. **Expose Pod hoặc Deployment dưới dạng Service**: Để biến pod hoặc deployment thành một dịch vụ, bạn sử dụng lệnh:
   ```bash
   kubectl expose <pod|deployment> <tên-pod|deployment>
   ```

3. **Tự động mở rộng (Auto-scaling)**: Bạn có thể sử dụng lệnh auto-scaling để tự động mở rộng và đặt các pod phía sau một load balancer:
   ```bash
   kubectl autoscale deployment <tên-deployment> --min=1 --max=5
   ```
   Kubernetes sẽ tự động tạo một load balancer và cấu hình tất cả cho bạn.

4. **Mở rộng quy mô ngang (Horizontal Scaling)**: Bạn có thể thay đổi số lượng bản sao pod (replica) để mở rộng quy mô khi có tải cao:
   ```bash
   kubectl scale deployment <tên-deployment> --replicas=3
   ```

5. **Thêm Metadata với `annotate`**: Bạn có thể thêm thông tin metadata như công ty tạo, thời gian tạo và ứng dụng sử dụng pod:
   ```bash
   kubectl annotate pod <tên-pod> company="MyCompany" created="2025-01-08"
   ```
   Lưu ý rằng thông tin này sẽ không được lưu trong đối tượng Kubernetes, nhưng thông tin chú thích sẽ gắn liền với đối tượng miễn là đối tượng đó còn tồn tại.

6. **Sử dụng Labels trong Kubernetes**: Label là thành phần quan trọng trong Kubernetes, giúp liên kết dịch vụ với deployments và pods. Labels cho phép Kubernetes theo dõi và quản lý các pod một cách hiệu quả hơn. Bạn có thể thêm hoặc xóa label khi tạo pod hoặc deployment.

7. **Xóa Đối Tượng**: Để xóa một đối tượng Kubernetes, bạn sử dụng lệnh:
   ```bash
   kubectl delete <resource> <name>
   ```
   Lệnh này sẽ xóa đối tượng khỏi cụm Kubernetes và loại bỏ thông tin liên quan từ cơ sở dữ liệu, khiến garbage collector hoạt động và dọn dẹp các tài nguyên liên quan.

8. **Xem Thông Tin về Đối Tượng Kubernetes**:
   - **`describe`**: Lệnh này cho phép bạn xem chi tiết về một đối tượng cụ thể (ví dụ: pod):
     ```bash
     kubectl describe pod <tên-pod>
     ```
     Bạn có thể sử dụng lệnh này để hiểu rõ hơn về pod, ví dụ như thông tin về container image mà pod đang sử dụng.

9. **Lấy Thông Tin Pod dưới Dạng YAML**: Bạn có thể sử dụng lệnh `get` để lấy thông tin pod dưới dạng YAML và tái sử dụng YAML đó:
   ```bash
   kubectl get pod <tên-pod> -o yaml
   ```
### **2. Khái Niệm về Pod trong Kubernetes**:

Chúng ta đã thảo luận về pod trước đây. Một pod có thể chứa một hoặc nhiều container. Khi tạo một pod, bạn quyết định số lượng container muốn đưa vào pod đó. Trong một số trường hợp, ứng dụng có thể cần thêm các thành phần như logging, v.v., và bạn có thể thêm chúng vào trong pod. Sau đó, bạn có thể tạo một deployment trên pod đó để đảm bảo tính mở rộng, tăng dung lượng khi cần thiết.

***Quản Lý Sức Khỏe và Quá Trình trong Kubernetes:***

Kubernetes sẽ báo cáo trạng thái sức khỏe của mỗi quá trình đang chạy trong cụm. Mỗi pod có một container và container chỉ chạy một quá trình. Điều này có nghĩa là pod chứa một container chỉ chạy một quá trình duy nhất và không làm quá nhiều việc, nhằm giảm thiểu hoạt động không cần thiết.

Khi một pod được tạo, nó sẽ nhận một địa chỉ IP riêng biệt, giúp pod này giao tiếp với các pod khác thông qua địa chỉ IP đó. Cấu hình trong pod giúp định hình cách mà container trong pod hoạt động, ví dụ như yêu cầu về RAM, CPU, hoặc vị trí node cụ thể mà pod nên chạy (node affinity). Bạn cũng có thể sử dụng bộ nhớ ngoài thông qua persistent volume, điều này đảm bảo rằng dữ liệu vẫn tồn tại ngay cả khi pod bị tắt và một pod mới được tạo.

***Tính Năng của Pod:***
1. **Nền tảng mạng đơn giản**: Pod giúp đơn giản hóa nhiều vấn đề mạng. Khi tất cả container trong một pod sử dụng cùng một network namespace và cùng một địa chỉ IP, chúng có thể giao tiếp với nhau mà không cần phải lo lắng về các vấn đề mạng phức tạp.
   
2. **Giao tiếp giữa các Pod**: Các pod có thể kết nối với nhau thông qua địa chỉ IP của chúng. Bên cạnh đó, bạn có thể tạo các dịch vụ ngoài pod, ví dụ như hosting ứng dụng HTTP và mở cổng 80 cho phép các yêu cầu từ bên ngoài đi vào.

3. **Cơ chế Mở rộng và Quản lý Pod**: Pod hỗ trợ dễ dàng mở rộng, bạn có thể tạo thêm pod hoặc tự động tắt pod khi cần thiết. Một cách thông dụng để sử dụng tính năng này là thông qua deployment, nơi bạn có thể tăng dung lượng của hệ thống bằng cách tăng số lượng pod.

***Định Nghĩa và Quản Lý Pod:***
- **Tạo Pod**: Bạn có thể tạo một pod trực tiếp bằng cách sử dụng lệnh:
  ```bash
  kubectl run <tên-pod> --image=<image-name>
  ```

- **Pod trong Deployment, Job, và DaemonSet**: Khi tạo một deployment, job, hoặc daemonset, Kubernetes sẽ tạo pod theo các định nghĩa trong các cấu hình của chúng. Các đối tượng này đều cần sử dụng pod để có thể chạy container.

- **Pod Template**: Trong YAML file, khi bạn tạo một deployment hoặc job, bạn có thể thấy một "pod template". Đây là nơi bạn định nghĩa các chi tiết của pod, ví dụ như tên container, image, và các yêu cầu về tài nguyên.

***Pod với Nhiều Container:***
Pod có thể chứa nhiều container, điều này giúp các container trong cùng một pod chia sẻ tài nguyên và phụ thuộc vào nhau. Một ví dụ phổ biến là khi có một container chuyên về việc nhận file từ mạng và lưu vào persistent volume, trong khi một container khác sẽ đọc những file đó từ persistent volume và gửi ra ngoài.

***Ví Dụ về Multi-Container Pod:***
- Một container làm nhiệm vụ nhận và lưu file vào persistent volume, trong khi container còn lại đọc và xử lý file đó.
- Container thứ hai giúp web server giảm tải công việc, vì container này chuyên dụng cho việc tải file từ thế giới bên ngoài và lưu vào bộ nhớ trong, trong khi web server chỉ cần xử lý các file đã sẵn sàng.

Việc sử dụng multi-container pod giúp tối ưu hóa hoạt động của từng container, đồng thời chia sẻ tài nguyên hiệu quả hơn.

### **3. Kubernetes Deployment**:

Trong môi trường sản xuất thực tế, chúng ta thường không tạo một pod đơn lẻ mà luôn tạo pod bên trong một deployment. Đây là cách mà Kubernetes tổ chức. Một deployment sẽ chứa một số thông tin quan trọng:

1. **Số lượng bản sao**: Deployment sẽ quyết định số lượng bản sao của pod cần chạy, ví dụ như một bản sao, hai bản sao hoặc nhiều hơn. 
2. **Pod template**: Định nghĩa pod thông qua template, giống như cách chúng ta đã thấy trong ví dụ YAML trước đó, nơi pod được tạo ra trong job.

***Quản Lý Pod trong Deployment:***

Khi tạo một deployment, nó sẽ tạo ra một hoặc nhiều pod, và các pod này có thể được phân phối trên nhiều node khác nhau. Deployment sử dụng label để giám sát tình trạng sức khỏe của các pod. Nếu số lượng pod giảm hoặc một pod bị hỏng, deployment sẽ tự động tạo lại pod để đảm bảo số lượng pod theo yêu cầu. Ví dụ, nếu bạn yêu cầu ít nhất 3 pod, deployment sẽ tự động duy trì số lượng đó.

***Quản Lý Phiên Bản và Rollback:***

Deployment có khả năng quay lại trạng thái trước đó nếu có sự cố xảy ra sau khi nâng cấp. Bạn có thể sử dụng cơ chế **rollout** để quay lại phiên bản trước đó hoặc triển khai một phiên bản mới mà không làm gián đoạn dịch vụ. Điều này giúp hệ thống luôn duy trì hoạt động mà không bị gián đoạn.

***Cập Nhật và Mở Rộng Deployment:***

1. **Tự động tạo lại pod**: Nếu một pod bị hỏng hoặc không hoạt động, deployment sẽ tự động tạo lại pod mà không cần can thiệp thủ công.
2. **Chạy nhiều container trong mỗi pod**: Mỗi pod trong deployment sẽ có cùng một template pod, nhưng chúng có thể được triển khai trên các node khác nhau, tùy thuộc vào tài nguyên và cấu hình đã định.

***Quản Lý Số Lượng Replica:***

Khi tạo một deployment, bạn có thể cấu hình số lượng replica (bản sao) cần thiết. Nếu số lượng pod cần thay đổi, bạn có thể thay đổi số lượng replica trong YAML file hoặc sử dụng lệnh dòng lệnh để cập nhật.

Ví dụ: Nếu bạn bắt đầu với 2 replica và sau đó cần 10 replica, bạn có thể chỉnh sửa file YAML hoặc sử dụng lệnh dòng lệnh để thay đổi số lượng replica.

***Lợi Ích và Tính Linh Hoạt của Deployment:***
- **Mở rộng và thu hẹp tự động**: Bạn có thể tăng hoặc giảm số lượng pod dễ dàng mà không gặp phải sự gián đoạn lớn.
- **Cập nhật mà không gián đoạn**: Deployment sẽ cập nhật từng pod một và đảm bảo rằng người dùng cuối không bị ảnh hưởng bởi quá trình nâng cấp.
- **Quản lý sự cố**: Nếu có sự cố với bản cập nhật mới, bạn có thể quay lại phiên bản cũ hoặc điều chỉnh số lượng pod và replica.

### **4. Kubernetes Replica Set**:

1. **Khái niệm**:  
   - **Replica Set** là thành phần quan trọng trong Kubernetes giúp đảm bảo các pod luôn chạy. Nó dùng **pod template** để tạo các pod mới khi cần thiết.

2. **Cách hoạt động**:  
   - Khi định nghĩa một Replica Set, bạn định nghĩa số lượng pod mong muốn (desired replicas).  
   - **Labels** và **selectors** là cơ chế kết nối giữa Replica Set và các pod mà nó quản lý. Replica Set sử dụng selector để đọc label trên pod và xác định pod nào thuộc sự quản lý của nó.  
   - Nếu số lượng pod hiện tại thấp hơn số lượng mong muốn, Replica Set tự động tạo thêm pod mới để đạt số lượng cần thiết.

3. **Tự động duy trì trạng thái**:  
   - Replica Set liên tục quan sát các pod và tự động thay thế bất kỳ pod nào bị lỗi hoặc bị xóa, đảm bảo luôn có đúng số lượng pod đang hoạt động.

4. **Kết hợp với Deployment**:  
   - Khi bạn tạo một **Deployment**, Kubernetes tự động tạo ra một Replica Set để quản lý các pod trong Deployment đó.  
   - Deployment giúp duy trì và cập nhật Replica Set một cách dễ dàng.

5. **Tầm quan trọng của Labels**:  
   - Labels tuy chỉ là chuỗi văn bản đơn giản nhưng đóng vai trò rất quan trọng trong việc liên kết và quản lý các thành phần của Kubernetes.  
   - Replica Set sử dụng labels để nhận diện các pod mà nó cần giám sát và duy trì.
     
### **5. Kiến trúc Công ty Streaming Nhạc Sử Dụng Kubernetes**:

Dưới đây là phác thảo kiến trúc tổng quát minh họa cách một công ty streaming nhạc có thể sử dụng Kubernetes để quản lý hạ tầng của mình:

**1. Kiến trúc Microservices**  
Công ty sử dụng kiến trúc microservices, trong đó ứng dụng được chia nhỏ thành các dịch vụ độc lập và kết nối lỏng lẻo.  
- Mỗi dịch vụ đảm nhận một chức năng cụ thể (ví dụ: xác thực người dùng, gợi ý nhạc, quản lý danh sách phát).

**2. Container hóa**  
Công ty container hóa các microservices bằng Docker hoặc công nghệ tương tự.  
- Mỗi microservice được đóng gói thành một container bao gồm cả các phụ thuộc, giúp đảm bảo tính di động và đồng nhất trên mọi môi trường.

**3. Điều phối với Kubernetes**  
Kubernetes được sử dụng làm nền tảng điều phối để quản lý hạ tầng container hóa.  
- Các cụm Kubernetes bao gồm các **master node** và **worker node**, được phân bố trên nhiều vùng khả dụng (availability zones) để tăng tính sẵn sàng và khả năng chịu lỗi.

**4. Triển khai (Deployment)**  
Công ty sử dụng tài nguyên **Kubernetes Deployment** để định nghĩa trạng thái mong muốn của các microservices.  
- Kubernetes tự động lập lịch và triển khai các container dựa trên cấu hình Deployment, đảm bảo số lượng bản sao (replica) luôn chạy đúng với mong muốn.

**5. Tự động mở rộng (Scaling)**  
Công ty tận dụng **Kubernetes Horizontal Pod Autoscaler (HPA)** để tự động mở rộng số lượng pod dựa trên mức sử dụng CPU hoặc các chỉ số tùy chỉnh.  
- Kubernetes tự động điều chỉnh số lượng container đang chạy để đáp ứng nhu cầu lưu lượng thay đổi, tối ưu hóa việc sử dụng tài nguyên.

**6. Khám phá dịch vụ và cân bằng tải**  
- **Kubernetes Services** hoạt động như bộ cân bằng tải nội bộ, định tuyến lưu lượng đến các pod tương ứng.  
- Các microservices giao tiếp với nhau thông qua **Kubernetes Services**, giúp đơn giản hóa việc khám phá dịch vụ và cân bằng tải.

**7. Giám sát và ghi log**  
Công ty sử dụng các giải pháp giám sát và ghi log tích hợp với Kubernetes, như **Prometheus** và **Fluentd**, để thu thập và phân tích dữ liệu từ các cụm Kubernetes.  
- **Kubernetes Dashboard** hoặc các công cụ giám sát khác cung cấp khả năng hiển thị về tình trạng và hiệu suất của các microservices.

**8. Tích hợp liên tục và triển khai liên tục (CI/CD)**  
Kubernetes được tích hợp với quy trình CI/CD để tự động hóa các bước xây dựng, kiểm thử và triển khai.  
- Khi có thay đổi trong microservices, pipeline CI/CD sẽ tự động tạo hình ảnh container, chạy kiểm thử và triển khai phiên bản mới lên cụm Kubernetes.

**9. Khả năng chịu lỗi và phục hồi (Fault Tolerance & Resilience)**  
Công ty triển khai các tính năng của Kubernetes như **PodDisruptionBudgets** và **ReplicaSets** để đảm bảo khả năng chịu lỗi và phục hồi.  
- Kubernetes tự động xử lý các lỗi pod bằng cách khởi động lại hoặc lên lịch lại pod để duy trì mức độ sẵn sàng mong muốn.

### **6. Kubernetes Services**:
**1. Giới thiệu về Kubernetes Service**  
- Trong cụm Kubernetes, bạn có các **máy ảo** (virtual machines) và **pods** chạy container bên trong cụm đó.  
- Các máy ảo này có thể là **worker node** hoặc **master node**, và chúng đều là một phần của cụm Kubernetes.  
- Khi bạn tạo một **pod** và muốn **expose** (mở) nó ra ngoài cụm Kubernetes, bạn cần một thành phần gọi là **service**.  
- Hãy coi **service** như một phương thức giúp khám phá và kết nối mạng giữa các thành phần bên trong và bên ngoài cụm Kubernetes.

**2. Chức năng của Kubernetes Service**  
- **Service** giúp **expose endpoint** (điểm cuối) của một pod, ví dụ như một trang web hoặc API thông qua giao thức HTTP.  
- **Service** là một thành phần trong Kubernetes, tương tự như **deployment**, **replica set** hoặc **pod**.  
- Khi một **service** được tạo, nó sẽ gán một **tên** và một **địa chỉ IP cố định** (ClusterIP) cho một nhóm pods.  
  - Địa chỉ IP này không thay đổi miễn là **service** còn hoạt động.  
  - Nếu bạn xóa và tạo lại **service**, địa chỉ IP có thể thay đổi, nhưng khi **service** đang chạy, IP sẽ luôn cố định.  

**3. Các loại Kubernetes Service**  
1. **ClusterIP**  
   - Đây là loại mặc định, dùng để giao tiếp nội bộ giữa các thành phần trong cụm Kubernetes.  
   - Địa chỉ IP này chỉ có thể truy cập từ bên trong cụm.

2. **NodePort**  
   - Dùng để **expose** dịch vụ ra bên ngoài cụm thông qua một cổng tĩnh trên từng node.  
   - Mỗi node trong cụm Kubernetes là một máy ảo có địa chỉ IP riêng.  
   - Khi sử dụng **NodePort**, bạn có thể truy cập dịch vụ bằng cách sử dụng địa chỉ IP của node và số cổng được chỉ định.

3. **LoadBalancer**  
   - Thường dùng khi triển khai Kubernetes trên các nền tảng **cloud**.  
   - Loại **service** này cấp một địa chỉ IP công khai để người dùng bên ngoài có thể truy cập dịch vụ.

4. **ExternalName**  
   - Loại này trả về một bản ghi **CNAME** (Canonical Name), ánh xạ dịch vụ đến một tên miền bên ngoài được xác định trước.

**4. Cấu hình Service bằng YAML**  
Khi cấu hình một **service**, bạn định nghĩa loại service và các thông số cần thiết như cổng, cổng mục tiêu (target port), và **node port**. Ví dụ:  
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30007
```

- Trong cấu hình trên:  
  - **type**: `NodePort` định nghĩa loại service là NodePort.  
  - **port**: Cổng mà dịch vụ sẽ lắng nghe.  
  - **targetPort**: Cổng mà ứng dụng bên trong pod sẽ sử dụng.  
  - **nodePort**: Cổng mà mỗi node sẽ mở để cho phép truy cập từ bên ngoài.

### **7. Kubernetes Networking**:

**1. Tổng quan về mạng trong Kubernetes**  
Mô hình mạng của Kubernetes là một phương thức kết nối các thành phần trong cụm Kubernetes.  
- Sử dụng cấu trúc mạng phẳng (*flat network structure*), loại bỏ nhu cầu ánh xạ cổng giữa máy chủ và container.  

**2. Nhu cầu về mạng trong Kubernetes**  
- Kubernetes cho phép nhiều ứng dụng **chia sẻ tài nguyên trên cùng một máy**.  
- Việc phối hợp các cổng giữa nhiều nhà phát triển trở nên khó khăn do các ứng dụng khác nhau có thể yêu cầu các cổng giống nhau.  
- Do đó, khi chia sẻ máy, cần đảm bảo rằng không có hai ứng dụng nào sử dụng cùng một cổng.  
- Ngoài ra, người dùng cũng phải đối mặt với các vấn đề cấp cụm mà họ không thể kiểm soát được.  
- Hệ thống trở nên phức tạp bởi việc cấp phát cổng động. Các ứng dụng phải sử dụng các cổng như một cờ hiệu (*flag*) để giao tiếp.  
- Dịch vụ (*service*) cần biết cách tìm và kết nối với nhau. Máy chủ API (*API server*) phải biết cách chèn số cổng động vào các khối cấu hình.  

Để đơn giản hóa vấn đề, Kubernetes áp dụng một phương pháp khác, giúp loại bỏ các vấn đề về ánh xạ cổng và cấu hình thủ công.

**3. Yêu cầu cơ bản của mô hình mạng Kubernetes**  
Kubernetes đặt ra một số yêu cầu cơ bản cho việc triển khai mạng:  
1. **Pod-to-Pod Communication**  
   - **Tất cả các pod** có thể giao tiếp với nhau mà không cần sử dụng NAT (Network Address Translation).  
2. **Node-to-Pod Communication**  
   - **Tất cả các node** có thể giao tiếp với tất cả các pod mà không cần NAT.  
3. **Địa chỉ IP nhất quán**  
   - Địa chỉ IP mà một pod nhìn thấy phải giống với địa chỉ IP mà các pod khác nhìn thấy.  

Mô hình mạng này giúp việc triển khai ứng dụng trong Kubernetes trở nên dễ dàng và tương thích hơn với mục tiêu ban đầu của Kubernetes là chuyển đổi các ứng dụng từ máy ảo (VMs) sang container mà không gặp nhiều trở ngại.  

Nếu trước đây một ứng dụng đã chạy trên máy ảo với một địa chỉ IP cố định và có thể giao tiếp với các máy ảo khác, thì mô hình mạng của Kubernetes vẫn đảm bảo điều tương tự khi ứng dụng chuyển sang container.

**4. Các vấn đề mạng mà Kubernetes giải quyết**  
Kubernetes giải quyết ba loại vấn đề mạng chính:  

1. **Container-to-Container Communication**  
   - Được giải quyết thông qua các pod và mạng nội bộ (*localhost networking*).  
   - Các container trong cùng một pod có thể giao tiếp với nhau bằng cách sử dụng địa chỉ `localhost`.  

2. **Pod-to-Pod Communication**  
   - Giao tiếp giữa các pod được thiết lập **mặc định** mà không cần cấu hình thêm.  

3. **Pod-to-Service Communication**  
   - Kubernetes sử dụng thành phần **service** để quản lý giao tiếp giữa các pod và các dịch vụ khác nhau.  

4. **External Communication**  
   - Giao tiếp giữa internet bên ngoài và các dịch vụ bên trong cụm Kubernetes được quản lý bởi các loại **service** như `NodePort`, `LoadBalancer`, hoặc `Ingress`.

