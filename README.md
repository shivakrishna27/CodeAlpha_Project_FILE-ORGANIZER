# CodeAlpha_Project_FILE-ORGANIZER
import os
import shutil

def organize_files(directory):
    file_extensions = {
        'Images': ['.jpg', '.jpeg', '.png', '.gif', '.bmp'],
        'Documents': ['.pdf', '.doc', '.docx', '.txt', '.rtf'],
        'Videos': ['.mp4', '.avi', '.mkv', '.mov', '.wmv'],
        'Music': ['.mp3', '.wav', '.flac', '.aac'],
        'Archives': ['.zip', '.rar', '.7z', '.tar.gz']
    }

    for folder in file_extensions:
        folder_path = os.path.join(directory, folder)
        if not os.path.exists(folder_path):
            os.makedirs(folder_path)

    for filename in os.listdir(directory):
        if filename != os.path.basename(__file__): 
            file_path = os.path.join(directory, filename)
            if os.path.isfile(file_path):
             
                _, extension = os.path.splitext(filename)
                extension = extension.lower()

                for category, extensions in file_extensions.items():
                    if extension in extensions:
                        destination_folder = os.path.join(directory, category)
                        shutil.move(file_path, destination_folder)
                        print(f"Moved {filename} to {category} folder.")
                        break
                else:
                    print(f"No category found for {filename}.")

if __name__ == "__main__":
    directory_path = input("Enter the directory path to organize files: ")
    organize_files(directory_path)
