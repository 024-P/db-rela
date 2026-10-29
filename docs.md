# Football Ticket Booking & Souvenir Shop ⚽🎟️

# Team Members
# Owner : มีบุญจงเจริญ x หมอนทอง

1. KANCHAI UTHAIPAN (002)
2. NAPAT BOONMA (018)
3. TINNAPOB NAWACHITPHAIBOON (024)
4. PANNAWIT KOTPHU (043)
5. PARAPAT POUNGPIKUL (060)
6. MEEBOON HOONCHAREON (062)

# Data Dictionary

## Legends

| Keys & Constraints    | Description                                                                                                                                                |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SERIAL                | A type of value that will auto increment itself with each rows (entities) created, starting from 1. **DO NOT MODIFIED ANY ATTRIBUTES WITH THIS DATA TYPE** |
| VARCHAR(n)            | Basically a string value that can store up to `n` characters                                                                                               |
| INTEGER               | An integer value                                                                                                                                           |
| NUMERIC(x,y)          | A floating point value which contains `x` digits including the decimal digits, and `y` of the last digits are the decimal digits                           |
| BOOLEAN               | A boolean type that can only be `true` or `false`                                                                                                          |
| TIMESTAMP(0)          | A type of value that stores both date and time in a format of `YYYY-MM-DD HH24:mm:ss`                                                                      |
| DATE                  | A type of value that stores only the date in a format of `YYYY-MM-DD`                                                                                      |
| PK                    | Shorted from 'PRIMARY KEY,' implying that the attribute is the primary key of the entity. Assigning NOT NULL and UNIQUE automatically to the attribute     |
| FK                    | Shorted from 'FOREIGN KEY,' implying that this attribute is referenced to a primary key, inheriting values from it                                         |
| NN                    | Shorted from 'NOT NULL,' implying that the attribute MUST NOT be left emptied                                                                              |
| UNIQUE                | A constraint implying that the attribute MUST NOT have the same value as this attributes in the other entities in the same table                           |
| CHECK: `<expression>` | A constraint that implies that the expression must be `TRUE` in order for the attributes to be modified                                                    |
| DEFAULT: `<value>`    | A constraint that will add a default value to that attribute if one was not given                                                                          |
| REFERENCES: `t1(at2)` | A constraint showing that this attribute is a FOREIGN KEY, inheriting the value from `at2` from `t1`                                                       |



## 🗄️ Data Dictionary

## 1. user

An 'user' entity holds data about the users in the system including visitors, staffs, and admins.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **user_id** | **SERIAL** | **User's UID** | **PK** | |
| role | VARCHAR(50) | User's role (Visitor, Staff, Admin) | NN | |
| first_name | VARCHAR(255) | User's firstname | NN | |
| last_name | VARCHAR(255) | User's lastname | NN | |
| birthDate | DATE | User's date of birth | | |
| email | VARCHAR(255) | User's email | NN, UNIQUE | |
| phone | VARCHAR(20) | Phone number | NN | |
| password | VARCHAR(255) | User's Password | NN | |
| province | VARCHAR(100) | User's province | | |
| city | VARCHAR(100) | User's city or district | | |
| postalcode | VARCHAR(10) | User's postal code | | |
| startDate | TIMESTAMP(0) | User's account creation timestamp | NN, DEFAULT: `CURRENT_TIMESTAMP` | |
| expireDate | TIMESTAMP(0) | User's account expiration date | | |


## 2. seat

A 'seat' entity holds data about the available seats and their pricing in the stadium.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **seat_no** | **VARCHAR(10)** | **Seat number (e.g., A01, C15)** | **PK** | |
| type_no | INT | Type number (0 , 1) | NN, REFERENCES: `seat_type(type_no)` | FK |
| zone | VARCHAR(10) | Zone of the seat (A, B, C, D) | NN | |
| row | VARCHAR(5) | Row of the seat | NN | |

## 3. seat_type

A 'seat_type' entity holds data about the available types of seats and their pricing in the stadium.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **type_no** | **INT** | **Type number (0 , 1)** | **PK** | |
| type_name | VARCHAR(50) | Name Type of seat (REGULAR, VIP) | NN | |
| price | INT | Price of the seat in THB | NN | |

## 4. match

A 'match' entity holds data about the scheduled football matches.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **match_no** | **SERIAL** | **Match ID** | **PK** | |
| match_name | VARCHAR(50) | Match name | NN | |


## 5. match_detail

A 'match_detail' entity holds data about the detail football matches.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **match_detail_id** | **SERIAL** | **Match Detail ID** | **PK** | |
| match_no | INT | ID of the match | NN, REFERENCES: `match(match_no)` | FK |
| home_team_id | INT | Team ID | NN, REFERENCES: `team(team_id)` | FK |
| away_team_id | INT | Team ID | NN, REFERENCES: `team(team_id)` | FK |
| matchDate | TIMESTAMP(0) | date of the match | NN | |
| matchStart | TIMESTAMP(0) | Start date and time of the match | NN | |
| matchEnd | TIMESTAMP(0) | End date and time of the match | NN | |
| matchIMG | VARCHAR(50) | URL or path to the match banner image | | |


## 6. team

a 'team' entity holds data about the team.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **team_id** | **SERIAL** | **Team ID** | **PK** | |
| team_name | VARCHAR(100) | team name | NN | |

## 7. ticket

A 'ticket' entity holds data about the tickets booked by users.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **ticket_id** | **SERIAL** | **Ticket ID** | **PK** | |
| cart_no | INT | ID of the cart | NN, REFERENCES: `cart(cart_no)` | FK |
| seat_no | VARCHAR(10) | ID of the booked seat | NN, REFERENCES: `seat(seat_no)` | FK |
| match_no | INT | ID of the match | NN, REFERENCES: `match(match_no)` | FK |
| expire_date | TIMESTAMP(0) | Expiration time of the ticket | NN | |
| start_date | TIMESTAMP(0) | Valid from time | NN | |
| status | VARCHAR(50) | Ticket status (Active, Used, Cancelled) | NN, DEFAULT: `'Active'` | |



## 8.  discount

A 'discount' entity holds data about discount codes.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **discountid** | **SERIAL** | **Discount ID** | **PK** | |
| discountCode | VARCHAR(50) | The string code applied by the user | NN, UNIQUE | |
| used | BOOLEAN | Indicates if the discount has been used | NN, DEFAULT: `FALSE` | |


## 9. cart

A 'cart' entity holds data about the user's booking/shopping session.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **cart_no** | **SERIAL** | **Cart ID** | **PK** | |
| userID | INT | ID of the user owning the cart | NN, REFERENCES: `user(user_id)` | FK |
| discountID | INT | ID of the applied discount | REFERENCES: `discount(discountid)` | FK |
| paid | BOOLEAN | Payment status of the cart | NN, DEFAULT: `FALSE` | |
| paidDate | TIMESTAMP(0) | Payment date of the cart | NN | |
| createdDate | TIMESTAMP(0) | Created cart date | NN | |
| totalprice | INT | Total price | NN | |

## 10. product

A 'product' entity holds data about souvenir items available for purchase.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **prodID** | **SERIAL** | **Product ID** | **PK** | |
| prod_name | VARCHAR(255) | Name of the souvenir product | NN | |
| price | INT | Price of the product in THB | NN | |


## 11. product_order

A 'product_order' entity holds data about the specific products added to a cart.

| Attribute | Data Type | Description | Keys & Constraints | Note |
| :--- | :--- | :--- | :--- | :--- |
| **product_no** | **SERIAL** | **Order Item ID** | **PK** | |
| cart_no | INT | ID of the cart this order belongs to | NN, REFERENCES: `cart(cart_no)` | FK |
| prodID | INT | ID of the product ordered | NN, REFERENCES: `product(prodID)` | FK |
| quantity | INT | Quantity of the product ordered | NN, CHECK: `quantity > 0` | |
