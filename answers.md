**full_name** -
Direct PII	-
Drop or pseudonymize	-
Directly identifies an individual. 

**email** -
Direct PII -	
Drop	-
Unique identifier that directly links to a person.

**date_of_birth** -
Indirect PII	-
Mask -
Exact DOB can enable re-identification when combined with other fields.

**zip_code**	-
Indirect PII	-
Mask -
Partial ZIP reduces risk.

**job_title** -
Indirect PII	-
Mask	-
Rare or specific job titles can identify individuals.

**diagnosis_notes** -
Sensitive PII -
Mask -
May contain sensitive notes.


'''python
Violation 1: Ignoring API Rate Limits

    import requests
    import time

    records = []

    for page in range(1, 101):
        response = requests.get(API_URL, params={"page": page, "key": API_KEY})
    
    if response.status_code == 429:
        time.sleep(5) 
        continue

    data = response.json()
    records.extend(data["results"])
    
    time.sleep(1)  

Violation 2: Permanent Storage of Sensitive API Data

    def clean_record(record):
        return {
            "age": calculate_age(record["date_of_birth"]),
            "zip_prefix": record["zip_code"][:3],
            "diagnosis": record["diagnosis_notes"]
        }

    cleaned_records = [clean_record(r) for r in records]

    save_to_database(cleaned_records)
