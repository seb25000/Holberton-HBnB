HBnB, Diagramme de package, task 0 : 


0. High-Level Package Diagram :


![hbnb_diagramme_package_projet_1_task_0](https://github.com/user-attachments/assets/e90c3d18-4c77-4c8e-9458-d872cc253a36)



![Task_0_Diagramme_Package](https://github.com/user-attachments/assets/fa0a2097-ce0f-43b2-9eca-ad020cfde82f)



1. Detailed Class Diagram for Business Logic Layer :


![Task_1_Diagramme_Class](https://github.com/user-attachments/assets/378e9ea2-0326-453e-814f-45b54e7b4379)



2. Sequence Diagrams for API Calls :


![Task_2_Diagramme_Sequence](https://github.com/user-attachments/assets/32c6d4e8-b666-4014-a709-46a054e21309)



3. Documentation Compilation :


@startuml

!define RECTANGLE class

' Title and introduction
title Documentation Compilation for HBnB Project

' Introduction Section
section "Introduction" {
  note left of class Introduction
    The HBnB project aims to create an online platform for managing vacation rentals. 
    This technical document compiles the high-level architecture, business logic layer, 
    and API interaction flows, to guide the development process and provide a reference 
    for the implementation phases.
  end note
}

' High-Level Architecture Section
section "High-Level Architecture" {
  ' High-Level Package Diagram
  package "HBnB System Architecture" {
    RECTANGLE UserModule {
      class User
      class UserService
    }
    RECTANGLE ReservationModule {
      class Reservation
      class ReservationService
    }
    RECTANGLE PaymentModule {
      class Payment
      class PaymentService
    }
    RECTANGLE NotificationModule {
      class Notification
      class NotificationService
    }
    
    ' Relationships between packages
    UserModule -[hidden]-> ReservationModule
    ReservationModule -[hidden]-> PaymentModule
    PaymentModule -[hidden]-> NotificationModule
  }
  note left of UserModule
    The high-level architecture is based on a layered approach with 
    distinct modules for user management, reservations, payments, 
    and notifications.
  end note
}

' Business Logic Layer Section
section "Business Logic Layer" {
  ' Detailed Class Diagram
  package "Business Logic Layer" {
    RECTANGLE BusinessLogic {
      class User {
        +createUser()
        +authenticate()
        +getUserDetails()
      }
      class Reservation {
        +createReservation()
        +cancelReservation()
        +getReservationDetails()
      }
      class Payment {
        +processPayment()
        +refundPayment()
        +getPaymentStatus()
      }
      class Notification {
        +sendNotification()
        +getNotificationHistory()
      }
    }
    
    ' Relationships in the Business Logic Layer
    User "1" -- "1..*" Reservation : manages
    Reservation "1" -- "1..*" Payment : processes
    Payment "1" -- "1..*" Notification : triggers
  }
  note left of BusinessLogic
    The business logic layer manages the core functionality of the system, 
    including user management, reservation handling, payment processing, 
    and notification services.
  end note
}

' API Interaction Flow Section
section "API Interaction Flow" {
  ' Sequence Diagrams for API Calls
  actor User as "User"
  participant ReservationSystem as "Reservation API"
  participant PaymentSystem as "Payment API"
  participant NotificationSystem as "Notification API"
  
  User -> ReservationSystem : Create Reservation
  ReservationSystem -> PaymentSystem : Process Payment
  PaymentSystem -> NotificationSystem : Trigger Notification
  NotificationSystem -> User : Send Confirmation
  
  note right of User
    This sequence demonstrates the flow of interactions between the User 
    and the system for making a reservation, processing payment, 
    and receiving a notification.
  end note
}

' Explanatory Notes
section "Explanatory Notes" {
  note left of class Introduction
    The introduction provides an overview of the document's purpose, 
    describing the HBnB project and its key objectives.
  end note
  
  note left of UserModule
    The high-level package diagram illustrates the modular design of the HBnB system. 
    Each module encapsulates a specific domain of the system, allowing for 
    easy maintenance and scaling.
  end note
  
  note left of BusinessLogic
    The detailed class diagram showcases the business logic layer, 
    highlighting the core entities and their interactions. These entities 
    facilitate operations like reservation creation, payment handling, 
    and user management.
  end note
  
  note left of User
    The `User` class is responsible for creating and authenticating users 
    and managing their data. It interacts with the `Reservation` class to 
    manage user-specific reservations.
  end note
}

@enduml



