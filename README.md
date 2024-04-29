# Protecting Your REST API

## Stateful VS Stateless
- **Stateful** is type of authentication process that relies on maintaining a "state" or session throughout a user's interaction with a system or application.
In stateful authentication, the server keeps track of the user's identity and authentication status as they navigate through different parts of the system or perform various actions. **E.g. : Session**

- **Stateless** is type of authentication process in which each request from a client to a server must contain all the information needed to understand and verify the user's identity and access rights. 
In other words, the client is responsible for storing all the information and sending it to the server. **E.g. : JWT**

## Authentication VS Authorization
- **Authentication** is the process of verifying the identity of an individual, system, or entity to ensure that they are who they claim to be. Authentication typically involves the presentation of credentials, such as a username and password, which then checks the provided information against stored records to grant or deny access.

- **Authorization** is the process of determining what actions or operations an authenticated user, system, or entity is allowed to perform within a system, application, or resource.
User or entity is verified, and it involves granting or denying permissions and access rights based on the user's role, privileges, or the policies in place.
E.g. William may have privilege to read and delete, but Agus is only allowed to read the data


## Login Process
- Saat login, harus menyimpan hal-hal yang penting agar nanti bisa di identifikasi siapa user yang sedang login 
- JWT disini tugasnya untuk menggantikan session (soalnya session dianggap kurang aman, dan di refresh jg langsung hilang)
- jadi pada saat login , sekarang kita bisa membuat payload (data-data yang akan disimpan) yang berisi contohnya id yang lagi login, rolenya, dan usernamenya 
- Tidak seperti session , data2 yang akan disimpen itu ibaratnya di encrypt dulu (supaya lebih aman) dan dijadikan acesss token
- Karena kita sekarang udah gak server side rendering, udah jadi REST API, kita kirim access tokennya di res.statusnya

