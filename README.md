import tkinter as tk

def start_appointment_booking():
    appointment_frame.pack_forget()
    patient_details_frame.pack()

def show_doctor_details():
    patient_details_frame.pack_forget()
    doctor_details_frame.pack()

def confirm_appointment():
    confirmation_frame.pack()
    doctor_details_frame.pack_forget()
    # Add cancel button in confirmation page
    cancel_button = tk.Button(confirmation_frame, text="Cancel Appointment", command=cancel_booking)
    cancel_button.pack()

    # Start countdown for cancellation
    start_countdown(2 * 3600)  # 2 hours in seconds

def start_countdown(seconds):
    def update_timer():
        nonlocal seconds
        if seconds > 0:
            seconds -= 1
            countdown_label.config(text=f"Time remaining to cancel: {seconds // 3600} hours {seconds % 3600 // 60} minutes {seconds % 60} seconds")
            countdown_label.after(1000, update_timer)
        else:
            countdown_label.config(text="Time's up! Appointment cannot be cancelled.")
    
    update_timer()

def cancel_booking():
    # Code to cancel booking
    print("Booking Cancelled")
    confirmation_frame.pack_forget()
    appointment_frame.pack()

    # Display cancel frame
    cancel_frame = tk.Frame(root)
    cancel_frame.pack()
    cancel_label = tk.Label(cancel_frame, text="Your appointment is cancelled", font=("Helvetica", 14, "bold"), fg="red")
    cancel_label.pack(pady=10)
    thank_you_label = tk.Label(cancel_frame, text="Thank you!", font=("Helvetica", 12))
    thank_you_label.pack(pady=5)

root = tk.Tk()
root.title("Appointment booking page")

# Function to display confirmation note
def display_confirmation_note():
    confirmation_note = "Appointment will be cancelled within 2 hours from booking. Fee is $200. For any queries, contact 91919191919."
    confirmation_label.config(text=confirmation_note, font=("Helvetica", 12, "bold"))

# Appointment frame
appointment_frame = tk.Frame(root)
title_label = tk.Label(appointment_frame, text="Welcome to Vishnu Hospitals!", font=("Apricots", 25))
title_label.pack(pady=20)
instructions_label = tk.Label(appointment_frame, text="Start booking the slots:", font=("Helvetica", 15))
instructions_label.pack()
start_button = tk.Button(appointment_frame, text="Start appointment booking", command=start_appointment_booking)
start_button.pack(pady=20)
appointment_frame.pack()

# Patient details frame
patient_details_frame = tk.Frame(root)
name_label = tk.Label(patient_details_frame, text="Name:")
name_label.grid(row=0, column=0, pady=5)
name_entry = tk.Entry(patient_details_frame)
name_entry.grid(row=0, column=1, pady=5)
age_label = tk.Label(patient_details_frame, text="Age:")
age_label.grid(row=1, column=0, pady=5)
age_entry = tk.Entry(patient_details_frame)
age_entry.grid(row=1, column=1, pady=5)
gender_label = tk.Label(patient_details_frame, text="Gender:")
gender_label.grid(row=2, column=0, pady=5)
gender_entry = tk.Entry(patient_details_frame)
gender_entry.grid(row=2, column=1, pady=5)
address_label = tk.Label(patient_details_frame, text="Address:")
address_label.grid(row=3, column=0, pady=5)
address_entry = tk.Entry(patient_details_frame)
address_entry.grid(row=3, column=1, pady=5)
disease_label = tk.Label(patient_details_frame, text="Disease:")
disease_label.grid(row=4, column=0, pady=5)
disease_entry = tk.Entry(patient_details_frame)
disease_entry.grid(row=4, column=1, pady=5)
mobile_label = tk.Label(patient_details_frame, text="Mobile number:")
mobile_label.grid(row=5, column=0, pady=5)
mobile_entry = tk.Entry(patient_details_frame)
mobile_entry.grid(row=5, column=1, pady=5)

# Buttons for navigation
next_button = tk.Button(patient_details_frame, text="Next", command=show_doctor_details)
next_button.grid(row=6, column=1, pady=10)

# Doctor details frame
doctor_details_frame = tk.Frame(root)
doctor_details_label = tk.Label(doctor_details_frame, text="Doctor Details", font=("Helvetica", 15))
doctor_details_label.pack(pady=10)

def confirm_doctor_selection(doctor_name):
    confirmation_label.config(text=f"You have selected {doctor_name}.", font=("Helvetica", 12, "bold"))
    # Add navigation button
    next_button = tk.Button(doctor_details_frame, text="Next", command=confirm_appointment)
    next_button.pack()

# Adding doctor details
def add_doctor_details(doctor_name):
    select_label = tk.Label(doctor_details_frame, text=f"Doctor: {doctor_name}", font=("Helvetica", 12))
    select_label.pack()

    confirm_button = tk.Button(doctor_details_frame, text="Confirm Appointment", command=lambda: confirm_doctor_selection(doctor_name))
    confirm_button.pack(pady=5)

# Doctor details with confirm appointment button
add_doctor_details("Dr. Jahnavi - Dermatologist - Monday to Friday 10am to 10pm")
add_doctor_details("Dr. Harika - Cardiologist - Monday to Friday 10am to 10pm")
add_doctor_details("Dr. Sowjanya - Gynecologist - Monday to Friday 10am to 10pm")

# Confirmation note frame
confirmation_frame = tk.Frame(root)
confirmation_label = tk.Label(confirmation_frame, text="", font=("Helvetica", 12, "bold"))
confirmation_label.pack(pady=20)
countdown_label = tk.Label(confirmation_frame, text="", font=("Helvetica", 12))
countdown_label.pack(pady=10)
display_confirmation_note()

# Small note with contact information
contact_note = tk.Label(confirmation_frame, text="For further information, please call +91 987654321.", font=("Helvetica", 10))
contact_note.pack(pady=5)

root.mainloop()
