# read-file

        Introduction

The medical document maintenance project aims to streamline and organize healthcare documentation processes. It involves creating a system for efficient storage, retrieval, and management of patient records, medical histories, and related information. This project seeks to enhance accuracy, accessibility, and security of medical data, ultimately improving healthcare delivery and decision-making.

code 

import cv2
import pytesseract
import spacy


nlp = spacy.load("en_core_web_sm")


def extract_patient_details(text):
    doc = nlp(text)
    patient_details = {
        "Patient Name": "",
        "Age": "",
        "Phone Number": "",
        
    }

    for ent in doc.ents:
        if "Name" in ent.label_:
            patient_details["Patient Name"] = ent.text
        elif "Age" in ent.label_:
            patient_details["Age"] = ent.text
        elif "Phone" in ent.label_:
            patient_details["Phone Number"] = ent.text

    return patient_details


def extract_text_from_image(image_path):
    image = cv2.imread(image_path)
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    text = pytesseract.image_to_string(gray)
    return text

image_path = "C:/Users/VISHNU.S/Desktop/patient.jpg"
text_from_image = extract_text_from_image(image_path)
patient_details = extract_patient_details(text_from_image)

print("Extracted Patient Details:")
print(patient_details)
