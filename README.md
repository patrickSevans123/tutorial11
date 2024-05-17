##  Reflection on Hello Minikube
1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?<br>
Ya, log mengalami penambahan setiap kali kita membuka aplikasi. Hal ini terjadi karena logs akan bertambah setiap kali kita melakukan request GET. Berikut adalah perbedaan antara logs sebelum dan sesudah aplikasi di-expose sebagai sebuah service.<br>
Sebelum:
![Sebelum](img/logs-before-expose-service.png)
Sesudah:
![Sesudah](img/logs-after-expose-service.png)

2.  Notice that there are two versions of `kubectl get` invocation during this tutorial section.
The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?<br>
Fungsi opsi `-n` pada `kubectl get` adalah untuk mendefinisikan namespace yang resourcenya ingin kita lihat. Jadi, `kubectl get` tanpa `-n` hanya akan menunjukkan menampilkan informasi secara default, yaitu resource pada tempat kita bekerja sekarang. Di sisi lain, `kubectl get` dengan `-n` akan menampilkan deskripsi resource yang terkhusus pada namespace yang diinginkan saja.

##  Reflection on Rolling Update & Kubernetes Manifest File
1. What is the difference between Rolling Update and Recreate deployment strategy?
Perbedaan antara strategi rolling update dan recreate deployment terdapat pada bagaimana cara aplikasi di-deploy. Rolling update melakukan update pada aplikasi secara bertahap dimana update dilakukan bertahap pada subset-subset dari aplikasi. Di sisi lain, strategi recreate deployment dilakukan dengan deployment ulang dimana terdapat waktu dimana aplikasi down saat melakukan deployment ulang. Biasanya aplikasi yang digunakan secara masif menggunakan strategi rolling update untuk menjaga aplikasi agar tetap bisa digunakan.

2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.
Saya akan melakukan deploy Spring Petclinic REST dengan recreate deployment berdasarkan panduan dari laman berikut https://dev.to/cloudskills/kubernetes-deployment-strategy-recreate-3kgn
Berikut adalah tahapan yang dilakukan:
![Image](img/tutorial%2011%201.png)

Selanjutnya, saya mengedit deployment.apps untuk mengubah versi image menjadi 3.2.1 dan mengubah rollingupdate menjadi recreate/
![Image](img/tutorial%2011%20edited.png)

Ketika pods dihapus, pods yang lain langsung dibuat dan dirun untuk menggantikannya.

3. Prepare different manifest files for executing Recreate deployment strategy.
Saya menjalankan command berikut untuk membuat deployment2.yaml 
![Image](img/tutorial%2011%20no%203.png)

4.  What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking `kubectl apply-f` command) to the cluster.
Keuntungan dari menggunakan manifest files Kubernetes adalah kemampuan Kubernetes untuk membuat deployment.yaml secara instan, kita tidak perlu membuat yaml secara manual untuk melakukan deployment. Hal ini dapat membantu programmer untuk mempercepat dan meminimalisi error pada kode deployment.

