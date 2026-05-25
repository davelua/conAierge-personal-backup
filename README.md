# conAierge-personal-backup
```mermaid

classDiagram

    namespace 1_Core_Platform {
        class Hotels {
            +UUID hotel_id [PK]
            +String name
            +String location
            +String subscription_tier
            +Date created_at
            +Date updated_at
        }
        class Subscriptions {
            +UUID subscription_id [PK]
            +UUID hotel_id [FK]
            +String plan_type
            +String status
            +Date renewal_date
        }
    }

    namespace 2_User_Access_And_Security {
        class Users {
            +UUID user_id [PK]
            +String first_name
            +String last_name
            +String email
            +String password_hash
            +Date created_at
            +Date updated_at
        }
        class User_Hotel_Roles {
            +UUID role_id [PK]
            +UUID user_id [FK]
            +UUID hotel_id [FK]
            +String role_level
        }
    }

    namespace 3_AI_Settings_And_Knowledge {
        class Hotel_Bot_Configurations {
            +UUID config_id [PK]
            +UUID hotel_id [FK, Unique]
            +String bot_name
            +String primary_color_hex
            +String widget_greeting_message
            +Date updated_at
        }
        class Knowledge_Base_Documents {
            +UUID document_id [PK]
            +UUID hotel_id [FK]
            +String title
            +String content_url
            +Boolean is_active
            +Date last_trained_at
            +Date updated_at
        }
    }

    namespace 4_Hotel_Operations {
        class Guests {
            +UUID guest_id [PK]
            +UUID hotel_id [FK]
            +String first_name
            +String last_name
            +String email
            +String phone_number
            +String loyalty_tier
        }
        class Rooms {
            +UUID room_id [PK]
            +UUID hotel_id [FK]
            +String room_number
            +String room_type
            +String availability_status
        }
        class Reservations {
            +UUID reservation_id [PK]
            +UUID hotel_id [FK]
            +UUID guest_id [FK]
            +UUID room_id [FK]
            +Date check_in_date
            +Date check_out_date
            +String status
        }
    }

    namespace 5_CRM_And_AI_Analytics {
        class Guest_Inquiries {
            +UUID inquiry_id [PK]
            +UUID hotel_id [FK]
            +UUID reservation_id [FK]
            +String chat_transcript
            +String ai_classified_intent
            +Float sentiment_score
            +Boolean was_deflected
            +Date created_at
        }
    }

    %% Relationships
    Hotels "1" --> "*" Subscriptions : has
    Users "1" --> "*" User_Hotel_Roles : assigned_to
    Hotels "1" --> "*" User_Hotel_Roles : managed_by
    Hotels "1" --> "1" Hotel_Bot_Configurations : configures
    Hotels "1" --> "*" Knowledge_Base_Documents : owns
    Hotels "1" --> "*" Guests : registers
    Hotels "1" --> "*" Rooms : contains
    Hotels "1" --> "*" Reservations : holds
    Hotels "1" --> "*" Guest_Inquiries : receives
    Guests "1" --> "*" Reservations : makes
    Rooms "1" --> "*" Reservations : booked_for
    Reservations "1" --> "*" Guest_Inquiries : generates

    ```
