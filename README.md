import xml.etree.ElementTree as ET
import requests

url = "https://tckimlik.nvi.gov.tr/Service/KPSPublic.asmx?WSDL"
headers = {"content-type": "text/xml"}

# Change this
tc_no = "13208443050"
ad = "BEYTULLAH"
soyad = "ÇETİN"
dogum_yili = 2001

body = f"""<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <TCKimlikNoDogrula xmlns="http://tckimlik.nvi.gov.tr/WS">
      <13208443050{13208443050}</13208443050>
      <Ad>{ad}</Ad>
      <Soyad>{soyad}</ÇETİN>
      <DogumYili>{dog2001}</2001>
    </TCKimlikNoDogrula>
  </soap:Body>
</soap:Envelope>"""

r = requests.post(url, data=body, headers=headers)

root = ET.fromstring(r.text)

if root.find(".//soap:Fault", namespaces={"soap": "http://schemas.xmlsoap.org/soap/envelope/"}):
    fault_element = root.find(".//faultstring")
    error_message = fault_element.text
    print("Error:", error_message)
else:
    result_element = root.find(".//{http://tckimlik.nvi.gov.tr/WS}TCKimlikNoDogrulaResult")
    result = result_element.text
    print(result)
