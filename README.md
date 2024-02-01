# note_taker.py

import os

class NoteTaker:
    def __init__(self, notes_directory):
        self.notes_directory = notes_directory
        self.note_extension = ".txt"

        # Create the notes directory if it doesn't exist
        os.makedirs(self.notes_directory, exist_ok=True)

    def create_note(self, note_title, note_content):
        note_filename = note_title.replace(" ", "_") + self.note_extension
        note_filepath = os.path.join(self.notes_directory, note_filename)

        with open(note_filepath, 'w') as note_file:
            note_file.write(note_content)

        print(f"Note '{note_title}' created.")

    def view_notes(self):
        notes = [f.replace(self.note_extension, "") for f in os.listdir(self.notes_directory) if f.endswith(self.note_extension)]

        if notes:
            print("Available Notes:")
            for note in notes:
                print(f"- {note}")
        else:
            print("No notes available.")

    def view_note_content(self, note_title):
        note_filename = note_title.replace(" ", "_") + self.note_extension
        note_filepath = os.path.join(self.notes_directory, note_filename)

        if os.path.exists(note_filepath):
            with open(note_filepath, 'r') as note_file:
                note_content = note_file.read()
            print(f"\nNote Title: {note_title}\nNote Content:\n{note_content}")
        else:
            print(f"Note '{note_title}' not found.")

    def delete_note(self, note_title):
        note_filename = note_title.replace(" ", "_") + self.note_extension
        note_filepath = os.path.join(self.notes_directory, note_filename)

        if os.path.exists(note_filepath):
            os.remove(note_filepath)
            print(f"Note '{note_title}' deleted.")
        else:
            print(f"Note '{note_title}' not found.")

if __name__ == "__main__":
    notes_directory = "notes"  # Specify your notes directory here
    note_taker = NoteTaker(notes_directory)

    while True:
        print("\nOptions:")
        print("1. Create Note")
        print("2. View Notes")
        print("3. View Note Content")
        print("4. Delete Note")
        print("5. Exit")

        choice = input("Enter your choice (1/2/3/4/5): ")

        if choice == '1':
            note_title = input("Enter the note title: ")
            note_content = input("Enter the note content: ")
            note_taker.create_note(note_title, note_content)

        elif choice == '2':
            note_taker.view_notes()

        elif choice == '3':
            note_title = input("Enter the note title to view: ")
            note_taker.view_note_content(note_title)

        elif choice == '4':
            note_title = input("Enter the note title to delete: ")
            note_taker.delete_note(note_title)

        elif choice == '5':
            print("Exiting the note-taking application. Goodbye!")
            break

        else:
            print("Invalid choice. Please choose a valid option.")
