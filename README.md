# BambangShop Receiver App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a Rocket web framework skeleton that you can work with.

As this is an Observer Design Pattern tutorial repository, you need to implement a feature: `Notification`.
This feature will receive notifications of creation, promotion, and deletion of a product, when this receiver instance is subscribed to a certain product type.
The notification will be sent using HTTP POST request, so you need to make the receiver endpoint in this project.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Receiver" folder.

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    ROCKET_PORT=8001
    APP_INSTANCE_ROOT_URL=http://localhost:${ROCKET_PORT}
    APP_PUBLISHER_ROOT_URL=http://localhost:8000
    APP_INSTANCE_NAME=Safira Sudrajat
    ```
    Here are the details of each environment variable:
    | variable                | type   | description                                                     |
    |-------------------------|--------|-----------------------------------------------------------------|
    | ROCKET_PORT             | string | Port number that will be listened by this receiver instance.    |
    | APP_INSTANCE_ROOT_URL   | string | URL address where this receiver instance can be accessed.       |
    | APP_PUUBLISHER_ROOT_URL | string | URL address where the publisher instance can be accessed.       |
    | APP_INSTANCE_NAME       | string | Name of this receiver instance, will be shown on notifications. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)
3.  To simulate multiple instances of BambangShop Receiver (as the tutorial mandates you to do so),
    you can open new terminal, then edit `ROCKET_PORT` in `.env` file, then execute another `cargo run`.

    For example, if you want to run 3 (three) instances of BambangShop Receiver at port `8001`, `8002`, and `8003`, you can do these steps:
    -   Edit `ROCKET_PORT` in `.env` to `8001`, then execute `cargo run`.
    -   Open new terminal, edit `ROCKET_PORT` in `.env` to `8002`, then execute `cargo run`.
    -   Open another new terminal, edit `ROCKET_PORT` in `.env` to `8003`, then execute `cargo run`.

## Mandatory Checklists (Subscriber)
-   [ ] Clone https://gitlab.com/ichlaffterlalu/bambangshop-receiver to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [ ] Commit: `Create Notification model struct.`
    -   [ ] Commit: `Create SubscriberRequest model struct.`
    -   [ ] Commit: `Create Notification database and Notification repository struct skeleton.`
    -   [ ] Commit: `Implement add function in Notification repository.`
    -   [ ] Commit: `Implement list_all_as_string function in Notification repository.`
    -   [ ] Write answers of your learning module's "Reflection Subscriber-1" questions in this README.
-   **STAGE 3: Implement services and controllers**
    -   [ ] Commit: `Create Notification service struct skeleton.`
    -   [ ] Commit: `Implement subscribe function in Notification service.`
    -   [ ] Commit: `Implement subscribe function in Notification controller.`
    -   [ ] Commit: `Implement unsubscribe function in Notification service.`
    -   [ ] Commit: `Implement unsubscribe function in Notification controller.`
    -   [ ] Commit: `Implement receive_notification function in Notification service.`
    -   [ ] Commit: `Implement receive function in Notification controller.`
    -   [ ] Commit: `Implement list_messages function in Notification service.`
    -   [ ] Commit: `Implement list function in Notification controller.`
    -   [ ] Write answers of your learning module's "Reflection Subscriber-2" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Subscriber) Reflections

#### Reflection Subscriber-1
In this tutorial, we used RwLock<> to synchronise the use of Vec of Notifications. Explain why it is necessary for this case, and explain why we do not use Mutex<> instead?
> RwLock merupakan singkatan atas Read-Write Lock. Dia memastikan multiple threads untuk bisa membaca data dalam satu waktu tetapi hanya satu thread yang bisa melakukan write pada sekali waktu. Ini sangat cocok ketika kita punya kasus yang membutuhkan pembacaan data yang sering dan penulisan yang pada sekali-sekali saja, misalnya pada notifikasi. Program notification hanya menambahkan notifikasi yang baru sekali-sekali, tetapi sangat sering digunakan untuk proses read. RwLock akan mempercepat prosesnya. Mutex tidak dipilih karena mutex hanya memungkinkan satu data diakses dalam satu waktu tak peduli reading maupun writing (sesuai dengan namanya, mutual exclusion). Ini akan memperlama proses karena kita harus tetap menunggu meski padahal tidak ada proses writing yang sedang terjadi.

In this tutorial, we used lazy_static external library to define Vec and DashMap as a “static” variable. Compared to Java where we can mutate the content of a static variable via a static function, why did not Rust allow us to do so?
> Pada Rust kita tidak bisa langsung mengubah static variables kapanpun juga karena Rust sangat concern dengan pencegahan data races. Data race ini merupakan situasi ketika threads saling mengintervensi dan menyebabkan error atau hasil yang tak dapat diprediksi. Rust menggunakan aturan yang ketat untuk memastikan programnya aman dan data tidak corrupt ketika ada modifikasi yang melibatkan konkurensi. Lebih jauh, lazy_static diterapkan karena dia memungkinkan kita mendefinisikan variabel yang akan dibuat saat pertama kali dia diakses dan akan terus sama (immutable) setelahnya. Ini memungkinkan program kita lebih thread-safe.

#### Reflection Subscriber-2
Have you explored things outside of the steps in the tutorial, for example: src/lib.rs? If not, explain why you did not do so. If yes, explain things that you have learned from those other parts of code.
> Maaf, tapi saya belum coba mengeksplor hal tersebut. Saya ingin sekali mengeksplor masalah rust tapi tugas saya menumpuk terlalu banyak, dikarenakan terdapat kegiatan lain juga di luar kampus. Semoga melalui kelas adpro saya bisa semakin terpapar mengenai pemrograman dengan Rust maupun design pattern.


Since you have completed the tutorial by now and have tried to test your notification system by spawning multiple instances of Receiver, explain how Observer pattern eases you to plug in more subscribers. How about spawning more than one instance of Main app, will it still be easy enough to add to the system?
> Observer pattern menyederhanakan proses penambahan lebih banyak subscriber dalam sistem. Ketika terdapat informasi yang baru, semua orang yang telah melakukan subscribe akan mendapatkan informasi tanpa perlu memintanya. Saya tidak perlu melakukan pengubahan apapun pada sistem yang mengirimkan informasinya, maupun berurusan dengan subscriber lainnya. Saya hanya perlu menambahkan subscriber baru ke list dan mereka langsung mendapatkan update terbaru. Jika kita hendak spawn lebih dari satu instance dari main app, maka akan tetap bisa dikelola dengan baik. Setiap instance dari app bisa bertindak seolah mereka adalah sistem yang terpisah dengan Publisher dan Subscribernya sendiri. Sehingga, setiap app mengelola list nya sendiri dan mengirimkan notifikasinya secara independen. Ini menunjukan  sistem yang mudah di-scale up karena kita bisa mempunyai banyak aplikasi independen yang bekerja tanpa berintervensi dengan yang lainnya.

Have you tried to make your own Tests, or enhance documentation on your Postman collection? If you have tried those features, tell us whether it is useful for your work (it can be your tutorial work or your Group Project).
> Terus terang saya belum mencobanya tetapi sejauh yang saya baca, Postman ini sebenarnya menjadi fasilitator GUI untuk membantu kita berurusan dengan API. Postman akan memungkinkan saya saat bekerja dalam tim untuk group project terutama dalam hal  mencoba mengirimkan request, melihat respons, dan melakukan testing API tanpa harus menulis code tertentu.