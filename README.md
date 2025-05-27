# Simple-User-Login-System
# A simple user login and registration system written in python.
import os 
import csv
file_path = 'things.csv'
field = ["NAME","PASSWORD"]

class System:
    def __init__(self):
        print("====== HELLO, WELCOME HERE ======")
        pass

    def menu(self):
        try:
            print("  ------- CHOOSE FROM THE OPTIONS BELOW -------")
            Menu = ["REGISTER","LOGIN","SHOW ALL DETAILS","EXIT"]
            for idx,risen in enumerate(Menu,1):
                print(f"{idx}.    {risen}")
            
            menu_question = int(input("CHOICE: "))
            if menu_question == 1:
                self.register()

            if menu_question == 2:
                self.login()

            if menu_question == 3:
                self.show_details()

            if menu_question == 4:
                self.exiting()
                os._exit(0)
        except ValueError:
            print(" INVALID OPTION")

    def register(self):
        
        username = input("NAME: ").capitalize().strip()
        userpassword = input("PASSWORD: ").strip()
        with open(file_path, mode='a',newline='') as file:
            writer = csv.writer(file)
            writer.writerow([username,userpassword])
            print(" ******* ACCOUNT SUCCESSFULLY CREATED *******")


    def login(self):
        found = False
        new_name = input("NAME: ").strip().capitalize()
        new_password = input("PASSWORD: ").strip()
        with open(file_path,mode='r',newline='')as f:
            for line in f:
                if len(line.strip()) == 0 :
                    continue
                content = line.strip().split(',')
                if len(content) < 2:
                    continue

                name = content[0].strip()
                password = content[1].strip()

                if new_name == name and new_password == password:
                    print("******** LOGIN SUCCESSFUL ******")
                    found = True
        if not found :
                    print(" ********* ACCOUNT NOT FOUND //////////")

                    
                
                        
    def show_details(self):
        with open(file_path,mode='r',newline='') as file:
            read = csv.reader(file)
            for row in read:
                print(','.join(row))

    def exiting(self):
        print("Exiting........")
        pass

if __name__ == "__main__":
    system = System()
    system.menu()
