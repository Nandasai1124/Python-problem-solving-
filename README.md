# Python-problem-solving-
import requests
from bs4 import BeautifulSoup

def get_survey_numbers(district, mandal, village):
    url = "https://dharani.telangana.gov.in/knowLandStatus"
    data = {
        "districtCode": district,
        "mandalCode": mandal,
        "villageCode": village
    }

    response = requests.post(url, data=data)
    soup = BeautifulSoup(response.content, "html.parser")

    survey_numbers = []
    for option in soup.find("select", {"id": "ddlSurveyNo"}).find_all("option"):
        survey_numbers.append(option.text.strip())

    return survey_numbers

district = "your_district_code"
mandal = "your_mandal_code"
village = "your_village_code"

survey_numbers = get_survey_numbers(district, mandal, village)
print("Survey Numbers:")
for number in survey_numbers:
    print(number)
