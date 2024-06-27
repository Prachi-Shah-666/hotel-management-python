# hotel-management-python
<br>
#This is my first Git Repository. Here I am going to add Hotel Management Code written in Python Language.
#TAJ HOTEL MANAGEMENT SYSTEM
#WELCOME TO TAJ HOTEL
#MADE BY PRACHI SHAH
#CLASS 12th A1


from mysql.connector import connect, Error

# Establishing a connection to MySQL

try:
    mydb = connect(
        host="localhost",
        user="root",
        passwd="mysql"
    )
    mycursor = mydb.cursor()

    # Creating database "hotel"
    
    mycursor.execute("CREATE DATABASE IF NOT EXISTS hotel")
    mycursor.execute("USE hotel")

    # Creating tables
    
    mycursor.execute("CREATE TABLE IF NOT EXISTS bill (bill_id BIGINT(20) NOT NULL PRIMARY KEY AUTO_INCREMENT, "
                      "book_id BIGINT(20), "
                      "amount FLOAT(10,2), "
                      "bill_date DATE, "
                      "gst INT(10), "
                      "state INT(10))")

    mycursor.execute("CREATE TABLE IF NOT EXISTS booking (book_id BIGINT(20) NOT NULL PRIMARY KEY AUTO_INCREMENT, "
                      "room_id BIGINT(20), "
                      "cust_id BIGINT(20), "
                      "doo DATE, "
                      "dol DATE, "
                      "advance FLOAT(10,2))")

    mycursor.execute("CREATE TABLE IF NOT EXISTS customer (id BIGINT(20) NOT NULL PRIMARY KEY AUTO_INCREMENT, "
                      "name CHAR(50), "
                      "address CHAR(100), "
                      "phone CHAR(15), "
                      "email CHAR(80), "
                      "id_proof CHAR(20), "
                      "id_proof_no CHAR(25), "
                      "males INT(2), "
                      "females INT(2), "
                      "children INT(2))")

    mycursor.execute("CREATE TABLE IF NOT EXISTS rooms (id INT(10) NOT NULL PRIMARY KEY AUTO_INCREMENT, "
                      "room_no INT(4), "
                      "room_type CHAR(20), "
                      "room_rent FLOAT(10,2), "
                      "room_bed CHAR(20), "
                      "status CHAR(20))")

    mycursor.execute("CREATE TABLE IF NOT EXISTS setting (id INT(10) NOT NULL PRIMARY KEY AUTO_INCREMENT, "
                      "field_name CHAR(30), "
                      "value CHAR(100))")

    mydb.commit()

    print("*" * 25, "Hotel Management System", "*" * 25)
    print("1. Add New Room")
    print("2. Add Customer")
    print("3. Modify Room Information")
    print("4. Modify Customer Information")
    print("5. Room Booking")
    print("6. Bill Generation")
    print("7. Search Database")
    print("8. Report Menu")
    print("9. Settings")
    print("10. Close application")
    choice = int(input("Enter your choice: "))

    if choice == 1:
        user_room_no = input("Enter Room No: ")
        user_room_type = input("Enter Room type(AC/Delux/Super Delux): ")
        user_room_rent = input("Enter Room rent: ")
        user_room_bed = input("Enter No of beds(Single/Double/Triple): ")
        user_status = input("Enter Room Status(Free/Occupied): ")

        insert_query = "INSERT INTO rooms (room_no, room_type, room_rent, room_bed, status) " \
                       "VALUES (%s, %s, %s, %s, %s)"
        room_data = (user_room_no, user_room_type, user_room_rent, user_room_bed, user_status)

        mycursor.execute(insert_query, room_data)
        mydb.commit()
        print("Room inserted successfully")

    elif choice == 2:
        user_name = input("Enter Name of the customer: ")
        user_address = input("Enter Address of the customer: ")
        user_phone = input("Enter phone no of the customer: ")
        user_email = input("Enter email of the customer: ")
        user_proof = input("Enter customer proof: ")
        user_proof_no = input("Enter customer's proof no: ")
        males = input("Enter no of males: ")
        females = input("Enter no of females: ")
        children = input("Enter no of children: ")

        insert_query = "INSERT INTO customer (name, address, phone, email, id_proof, id_proof_no, males, females, children) " \
                       "VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s)"
        customer_data = (
            user_name, user_address, user_phone, user_email, user_proof, user_proof_no, males, females, children
        )

        mycursor.execute(insert_query, customer_data)
        mydb.commit()
        print("Customer inserted successfully")

    elif choice == 3:
        print("1. Room Type")
        print("2. Room Rent")
        print("3. Room Bed")
        print("4. Room Status")
        choice1 = int(input("Enter your choice: "))

        if choice1 == 1:
            room_id = input("Enter the ID of the room to modify: ")
            new_room_type = input("Enter the new room Type: ")

            update_query = "UPDATE rooms SET room_type = %s WHERE id = %s"
            update_data = (new_room_type, room_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

        elif choice1 == 2:
            room_id = input("Enter the ID of the room to modify: ")
            new_room_rent = input("Enter the new room rent: ")

            update_query = "UPDATE rooms SET room_rent = %s WHERE id = %s"
            update_data = (new_room_rent, room_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

        elif choice1 == 3:
            room_id = input("Enter the ID of the room to modify: ")
            new_room_bed = input("Enter the total no. of beds: ")

            update_query = "UPDATE rooms SET room_bed = %s WHERE id = %s"
            update_data = (new_room_bed, room_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

        elif choice1 == 4:
            room_id = input("Enter the ID of the room to modify: ")
            new_status = input("Enter the new status of the room (Free/Occupied): ")

            update_query = "UPDATE rooms SET status = %s WHERE id = %s"
            update_data = (new_status, room_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

    elif choice == 4:
        print("1. Customer Name")
        print("2. Customer Email")
        print("3. Customer Phone no.")
        print("4. Customer's Address")
        choice2 = int(input("Enter your choice: "))

        if choice2 == 1:
            customer_id = input("Enter the ID of the customer to modify: ")
            new_name = input("Enter the new name: ")

            update_query = "UPDATE customer SET name = %s WHERE id = %s"
            update_data = (new_name, customer_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

        elif choice2 == 2:
            customer_id = input("Enter the ID of the customer to modify: ")
            new_email = input("Enter the new email: ")

            update_query = "UPDATE customer SET email = %s WHERE id = %s"
            update_data = (new_email, customer_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

        elif choice2 == 3:
            customer_id = input("Enter the ID of the customer to modify: ")
            new_phone = input("Enter the new phone no.: ")

            update_query = "UPDATE customer SET phone = %s WHERE id = %s"
            update_data = (new_phone, customer_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

        elif choice2 == 4:
            customer_id = input("Enter the ID of the customer to modify: ")
            new_address = input("Enter the new address: ")

            update_query = "UPDATE customer SET address = %s WHERE id = %s"
            update_data = (new_address, customer_id)

            mycursor.execute(update_query, update_data)
            mydb.commit()
            print("Data modified successfully")

        else:
            print("Invalid choice")

    elif choice == 5:
        user_room_id = input("Enter Room ID: ")
        user_cust_id = input("Enter Customer ID: ")
        user_doo = input("Enter Date of Occupancy(yyyy-mm-dd): ")
        user_dol = input("Enter Date of leaving(yyyy-mm-dd): ")
        user_advance = input("Enter the amount paid in advance: ")

        insert_query = "INSERT INTO booking (room_id, cust_id, doo, dol, advance) " \
                       "VALUES (%s, %s, %s, %s, %s)"
        booking_data = (user_room_id, user_cust_id, user_doo, user_dol, user_advance)

        mycursor.execute(insert_query, booking_data)
        mydb.commit()
        print("Booking inserted successfully")

    elif choice == 6:
        user_book_id = input("Enter Booking ID: ")
        select_query = "SELECT * FROM customer WHERE id = (SELECT cust_id FROM booking WHERE book_id = %s)"
        select_data = (user_book_id,)

        mycursor.execute(select_query, select_data)
        customer_data = mycursor.fetchone()

        if customer_data:
            print("********** Bill**********")
            print("Booking ID:", user_book_id)
            print("Customer ID:", customer_data[0])
            print("Name:", customer_data[1])
            print("Address:", customer_data[2])
            print("Phone:", customer_data[3])
            print("Email:", customer_data[4])
            print("**************************")

        else:
            print("No customer found for the provided Booking ID")

    elif choice == 7:
        search_query = input("Enter the search query: ")
        select_query = "SELECT * FROM customer WHERE name LIKE %s OR address LIKE %s"
        select_data = (f"%{search_query}%", f"%{search_query}%")

        mycursor.execute(select_query, select_data)
        search_results = mycursor.fetchall()

        if search_results:
            print("---------- Search Results ----------")
            for result in search_results:
                print("Customer ID:", result[0])
                print("Name:", result[1])
                print("Address:", result[2])
                print("Phone:", result[3])
                print("Email:", result[4])
                print("--------------------------")

        else:
            print("No results found for the provided search query")

    elif choice == 8:
        print("1. Occupied Rooms Report")
        print("2. Available Rooms Report")
        print("3. Customer Report")
        print("4. Booking Report")
        print("5. Revenue Report")
        print("6. Exit")
        choice3 = int(input("Enter your choice: "))

        if choice3 == 1:
            
            # Occupied Rooms Report
            
            select_query = "SELECT * FROM rooms WHERE status = 'Occupied'"
            mycursor.execute(select_query)
            occupied_rooms = mycursor.fetchall()

            if occupied_rooms:
                print("----- Occupied Rooms Report -----")
                for room in occupied_rooms:
                    print("Room No:", room[1])
                    print("Room Type:", room[2])
                    print("Room Rent:", room[3])
                    print("--------------------------")

            else:
                print("No occupied rooms")

        elif choice3 == 2:
            
            # Available Rooms Report
            
            select_query = "SELECT * FROM rooms WHERE status = 'Free'"
            mycursor.execute(select_query)
            available_rooms = mycursor.fetchall()

            if available_rooms:
                print("----- Available Rooms Report -----")
                for room in available_rooms:
                    print("Room No:", room[1])
                    print("Room Type:", room[2])
                    print("Room Rent:", room[3])
                    print("--------------------------")

            else:
                print("No available rooms")

        elif choice3 == 3:
            
            # Customer Report
            
            select_query = "SELECT * FROM customer"
            mycursor.execute(select_query)
            customers = mycursor.fetchall()

            if customers:
                print("----- Customer Report -----")
                for customer in customers:
                    print("Customer ID:", customer[0])
                    print("Name:", customer[1])
                    print("Address:", customer[2])
                    print("Phone:", customer[3])
                    print("Email:", customer[4])
                    print("--------------------------")

            else:
                print("No customers")

        elif choice3 == 4:
            
            # Booking Report
            
            select_query = "SELECT * FROM booking"
            mycursor.execute(select_query)
            bookings = mycursor.fetchall()

            if bookings:
                print("----- Booking Report -----")
                for booking in bookings:
                    print("Booking ID:", booking[0])
                    print("Room ID:", booking[1])
                    print("Customer ID:", booking[2])
                    print("Date of Occupancy:", booking[3])
                    print("Date of Leaving:", booking[4])
                    print("Advance:", booking[5])
                    print("--------------------------")

            else:
                print("No bookings")

        elif choice3 == 5:
            
            # Revenue Report
            
            select_query = "SELECT SUM(advance) FROM booking"
            mycursor.execute(select_query)
            total_revenue = mycursor.fetchone()[0]
            print("----- Revenue Report -----")
            print("Total Revenue:", total_revenue)
            print("--------------------------")

        elif choice3 == 6:
            print("Exiting...")

        else:
            print("Invalid choice")

    elif choice == 9:
        
        # Settings
        
        hotel_name = input("Enter the hotel name: ")
        hotel_address = input("Enter the hotel address: ")
        update_query = "UPDATE setting SET field_name = %s, value = %s"
        mycursor.execute(update_query, (hotel_name, hotel_address))
        mydb.commit()

        print("Setting updated successfully")

    elif choice == 10:
        
        # This closes the function
        
        print("Closing application...")

except Error as e:
    print("Error:", e)

finally:
    if mydb.is_connected():
        mycursor.close()
        mydb.close()
 
