- '''
Doctor Class - ID, name, specialization, working time, qualification, and room number
'''

class Doctor:
    def __init__(self, doctor_id=None, name=None, specialization=None, working_time=None, qualification=None, room_number=None):

        self._doctor_id = doctor_id
        self._name = name
        self._specialization = specialization
        self._working_time = working_time
        self._qualification = qualification
        self._room_number = room_number

# Getter for getting values
    def get_doctor_id(self):
        return self._doctor_id

    def get_name(self):
        return self._name

    def get_specialization(self):
        return self._specialization

    def get_working_time(self):
        return self._working_time

    def get_qualification(self):
        return self._qualification

    def get_room_number(self):
        return self._room_number

# Setter for changing values
    def set_doctor_id(self, new_id):
        self._doctor_id = new_id

    def set_name(self, new_name):
        self._name = new_name

    def set_specialization(self, new_specialization):
        self._specialization = new_specialization

    def set_working_time(self, new_working_time):
        self._working_time = new_working_time

    def set_qualification(self, new_qualification):
        self._qualification = new_qualification

    def set_room_number(self, new_room_number):
        self._room_number = new_room_number

    def __str__(self):
        return f"{self._doctor_id}_{self._name}_{self._specialization}_{self._working_time}_{self._qualification}_{self._room_number}"


'''
DoctorManager Class
'''
#Reads from list of doctors
class DoctorManager:
    def __init__(self):
        self.doctors = []
        self.read_doctors_file()

# Format doctor info
    def format_dr_info(self, doctor):
        return str(doctor)

# User prompt for details on Doctor Manager class parameters
    def enter_dr_info(self):
        doctor_id = input("Enter the doctor’s ID: ")
        name = input("Enter the doctor’s name: ")
        specialization = input("Enter the doctor’s specialty: ")
        working_time = input("Enter the doctor’s timing (e.g., 7am-10pm): ")
        qualification = input("Enter the doctor’s qualification: ")
        room_number = input("Enter the doctor’s room number: ")
        return Doctor(doctor_id, name, specialization, working_time, qualification, room_number)

# Read doctor file and adds list
    def read_doctors_file(self):
        self.doctors = []
        with open('doctors.txt', 'r') as file:
            for line in file:
                doctor_data = line.strip().split('_')
                if len(doctor_data) == 6:
                    doctor = Doctor(*doctor_data)
                    self.doctors.append(doctor)

# Write list of doctors on file
    def write_list_of_doctors_to_file(self):
        with open('doctors.txt', 'w') as file:
            for doctor in self.doctors:
                file.write(self.format_dr_info(doctor) + '\n')

# Search for a doctor by ID and display doc info
    def search_doctor_by_id(self):
        doctor_id = input("Enter th\e doctor ID: ")
        for doctor in self.doctors:
            if doctor.get_doctor_id() == doctor_id:
                self.display_doctor_info(doctor)
                return
        print("Can't find the doctor with the same ID in the system")

# Search for a doctor by name and display
    def search_doctor_by_name(self):
        name = input("Enter the doctor name: ")
        for doctor in self.doctors:
            if doctor.get_name() == name:
                self.display_doctor_info(doctor)
                return
        print("Can't find the doctor with the same name in the system")

# Display the doc info using function to align text
    def display_doctor_info(self, doctor):
        print(f"{doctor.get_doctor_id():<5} {doctor.get_name():<20} {doctor.get_specialization():<15} {doctor.get_working_time():<15} {doctor.get_qualification():<15} {doctor.get_room_number()}")

# Edit doctor details
    def edit_doctor_info(self):
        doctor_id = input("Please enter the ID of the doctor that you want to edit their information: ")
        for doctor in self.doctors:
            if doctor.get_doctor_id() == doctor_id:
                doctor.set_name(input("Enter new Name: "))
                doctor.set_specialization(input("Enter new Specialty: "))
                doctor.set_working_time(input("Enter new Timing: "))
                doctor.set_qualification(input("Enter new Qualification: "))
                doctor.set_room_number(input("Enter new Room Number: "))
                print(f"Doctor whose ID is {doctor_id} has been edited")
                self.write_list_of_doctors_to_file()
                return
        print("Cannot find the doctor with the given ID")

# Display list of all doctors info in correct formatting
    def display_doctors_list(self):
        print(f"ID    Name                 Specialty       Timing          Qualification   Room Number")
        for doctor in self.doctors:
            self.display_doctor_info(doctor)
        print()

# Add a new doctor and write to file
    def add_dr_to_file(self):
        doctor = self.enter_dr_info()
        self.doctors.append(doctor)
        self.write_list_of_doctors_to_file()
        print(f"Doctor whose ID is {doctor.get_doctor_id()} has been added")


'''
Patient Class - pid, name, disease, gendr, and age
'''

class Patient:
    def __init__(self, pid=None, name=None, disease=None, gender=None, age=None):
        self.pid = pid
        self.name = name
        self.disease = disease
        self.gender = gender
        self.age = age

#Getter for returning values
    def get_pid(self):
        return self.pid

    def get_name(self):
        return self.name

    def get_disease(self):
        return self.disease

    def get_gender(self):
        return self.gender

    def get_age(self):
        return self.age

# Setter for modifying values
    def set_pid(self, new_pid):
        self.pid = new_pid

    def set_name(self, new_name):
        self.name = new_name

    def set_disease(self, new_disease):
        self.disease = new_disease

    def set_gender(self, new_gender):
        self.gender = new_gender

    def set_age(self, new_age):
        self.age = new_age

    def __str__(self):
        return f"{self.pid}_{self.name}_{self.disease}_{self.gender}_{self.age}"


'''
PatientManager Class
'''

#reads list of patients
class PatientManager:
    def __init__(self):
        self.patients = []
        self.read_patients_file()

# Format patient info
    def format_patient_info_for_file(self, patient):
        return str(patient)

# User input for patient values
    def enter_patient_info(self):
        pid = input("Enter Patient ID: ")
        name = input("Enter Patient name: ")
        disease = input("Enter Patient disease: ")
        gender = input("Enter Patient gender: ")
        age = input("Enter Patient age: ")
        return Patient(pid, name, disease, gender, age)

# Read patient data from file and appends
    def read_patients_file(self):
        self.patients = []
        with open('patients.txt', 'r') as file:
            for line in file:
                patient_data = line.strip().split('_')
                if len(patient_data) == 5:
                    patient = Patient(*patient_data)
                    self.patients.append(patient)

# Write list of patients
    def write_list_of_patients_to_file(self):
        with open('patients.txt', 'w') as file:
            for patient in self.patients:
                file.write(self.format_patient_info_for_file(patient) + '\n')

# Search for a patient by Id and display
    def search_patient_by_id(self):
        pid = input("Enter the Patient Id: ")
        for patient in self.patients:
            if patient.get_pid() == pid:
                self.display_patient_info(patient)
                return
        print("Can't find the Patient with the same ID in the system")

# Display patient info
    def display_patient_info(self, patient):
        print(f"{patient.get_pid():<5} {patient.get_name():<20} {patient.get_disease():<15} {patient.get_gender():<10} {patient.get_age()}")

# Edit patient details byr ID
    def edit_patient_info_by_id(self):
        pid = input("Please enter the ID of the Patient that you want to edit their information: ")
        for patient in self.patients:
            if patient.get_pid() == pid:
                patient.set_name(input("Enter new Name: "))
                patient.set_disease(input("Enter new Disease: "))
                patient.set_gender(input("Enter new gender: "))
                patient.set_age(input("Enter new Age: "))
                print(f"Patient whose ID is {pid} has been edited")
                self.write_list_of_patients_to_file()
                return
        print("Cannot find the patient with the given ID")

# Display all patients in correct format
    def display_patients_list(self):
        print(f"ID    Name                 Disease         Gender     Age")
        for patient in self.patients:
            self.display_patient_info(patient)
        print()

# Add patient to the list
    def add_patient_to_file(self):
        patient = self.enter_patient_info()
        self.patients.append(patient)
        self.write_list_of_patients_to_file()
        print(f"Patient whose ID is {patient.get_pid()} has been added")


'''
Management Class
'''

class Management:
    def __init__(self):
        self.doctor_manager = DoctorManager()
        self.patient_manager = PatientManager()

# Display main menu options
    def display_main_menu(self):
        print("Welcome to Alberta Hospital (AH) Management system")
        print("Select from the following options, or select 0 to stop:")
        print("1 - Doctors")
        print("2 - Patients")
        print("3 - Exit Program")

# Display doctors submenu options
    def display_doctor_menu(self):
        print("Doctors Menu:")
        print("1 - Display Doctors list")
        print("2 - Search for doctor by ID")
        print("3 - Search for doctor by Name")
        print("4 - Edit doctor information")
        print("5 - Add new doctor")
        print("6 - Return to Main Menu")

# Display patients submenu options
    def display_patient_menu(self):
        print("Patients Menu:")
        print("1 - Display Patients list")
        print("2 - Search for patient by ID")
        print("3 - Edit patient information")
        print("4 - Add new patient")
        print("5 - Return to Main Menu")

# Loop of the management program & defines OPTION selection
    def run(self):
        while True:
            self.display_main_menu()
#Introduce OPTION
            option = input("Please select an option: ")
            if option == "1":
                self.handle_doctor_menu()
            elif option == "2":
                self.handle_patient_menu()
            elif option == "3":
                self.exit_program()
                break
            else:
                print("Invalid option. Please try again.")

#Exit message
    def exit_program(self):
        print("Thank you for using the Alberta Hospital Management System. Goodbye!")

# Handle the doctor option menu
    def handle_doctor_menu(self):
        while True:
            self.display_doctor_menu()
            option = input("Please select an option: ")
            if option == "1":
                self.doctor_manager.display_doctors_list()
            elif option == "2":
                self.doctor_manager.search_doctor_by_id()
            elif option == "3":
                self.doctor_manager.search_doctor_by_name()
            elif option == "4":
                self.doctor_manager.edit_doctor_info()
            elif option == "5":
                self.doctor_manager.add_dr_to_file()
            elif option == "6":
                break
            else:
                print("Invalid option. Please try again.")

# Handle the patient option menu
    def handle_patient_menu(self):
        while True:
            self.display_patient_menu()
            option = input("Please select an option: ")
            if option == "1":
                self.patient_manager.display_patients_list()
            elif option == "2":
                self.patient_manager.search_patient_by_id()
            elif option == "3":
                self.patient_manager.edit_patient_info_by_id()
            elif option == "4":
                self.patient_manager.add_patient_to_file()
            elif option == "5":
                break
            else:
                print("Invalid option. Please try again.")


'''
Run the program
'''

if __name__ == "__main__":
    management_system = Management()
    management_system.run()
