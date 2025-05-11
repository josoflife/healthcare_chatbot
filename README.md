# healthcare_chatbot

knowledge_base = {
    "flu": ["fever", "cough", "sore_throat"],
    "common_cold": ["sneezing", "runny_nose", "mild_fever"],
    "malaria": ["fever", "chills", "sweating", "headache"],
    "covid19": ["fever", "cough", "shortness_of_breath", "loss_of_taste"],
    "strep_throat": ["sore_throat", "swollen_lymph_nodes", "fever"]
}


advice_base = {
    "flu": [
        "Rest and get plenty of sleep to help your body recover.",
        "Drink lots of fluids such as water, juice, and warm soups.",
        "Take over-the-counter medications like paracetamol to reduce fever and relieve pain.",
        "Use a humidifier or inhale steam to ease congestion and sore throat.",
        "Consult a healthcare provider if symptoms worsen or do not improve after a few days."
    ],
    "common_cold": [
        "Stay hydrated by drinking water and warm beverages.",
        "Rest as much as possible to help your immune system fight the infection.",
        "Use saline nasal drops or sprays to relieve nasal congestion.",
        "Gargle with warm salt water to soothe a sore throat.",
        "Avoid close contact with others to prevent spreading the cold."
    ],
    "malaria": [
        "Seek immediate medical attention for diagnosis and treatment.",
        "Take the full course of prescribed antimalarial medication.",
        "Rest in bed and avoid strenuous activity until you recover.",
        "Drink plenty of fluids to prevent dehydration.",
        "Use mosquito nets and repellents to avoid further mosquito bites."
    ],
    "covid19": [
        "Self-isolate and avoid contact with others to prevent spreading the virus.",
        "Monitor your temperature and oxygen levels regularly.",
        "Stay hydrated and eat nutritious food to support your recovery.",
        "Take over-the-counter medicines to relieve mild symptoms like fever or cough.",
        "Contact a healthcare provider immediately if you have difficulty breathing or persistent chest pain."
    ],
    "strep_throat": [
        "Take the full course of antibiotics as prescribed by your doctor.",
        "Rest your voice and avoid talking excessively.",
        "Drink warm liquids and eat soft foods to soothe your throat.",
        "Gargle with warm salt water several times a day.",
        "Avoid sharing utensils, cups, or food with others until you are no longer contagious."
    ]
}

def get_user_symptoms():
    print("\nWelcome to HealthBot!")
    print("Please enter your symptoms, separated by commas (e.g., fever, cough):")
    user_input = input("Symptoms: ").lower()
    symptoms = [s.strip() for s in user_input.split(',') if s.strip()]
    return symptoms

def infer_possible_diseases(user_symptoms):
    disease_matches = {}
    for disease, req_symptoms in knowledge_base.items():
        match_count = sum(symptom in user_symptoms for symptom in req_symptoms)
        if match_count > 0:
            disease_matches[disease] = match_count
    return disease_matches

def run_chatbot():
    user_symptoms = get_user_symptoms()
    disease_matches = infer_possible_diseases(user_symptoms)
    if disease_matches:
        print("\nBased on your symptoms, you might have (sorted by most matching symptoms):")
        
        for disease, count in sorted(disease_matches.items(), key=lambda x: x[1], reverse=True):
            total = len(knowledge_base[disease])
            print(f"- {disease.replace('_', ' ').title()} ({count}/{total} symptoms matched)")
            print("  Advice:")
            for advice in advice_base[disease]:
                print(f"    * {advice}")
    else:
        print("\nNo matching disease found.")
        print("Please consult a healthcare professional.")

if __name__ == "__main__":
    run_chatbot()
