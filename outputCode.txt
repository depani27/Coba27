import requests

def get_host():
    response = requests.get('https://xclite.netlify.app')
    if response.status_code == 200:
        return response.url
    else:
        raise Exception("Failed to get host from xclite.netlify.app")

def send_otp(phone_number):
    host = get_host()
    otp_url = f"{host}/api/users/otp"
    payload = {'phone_number': phone_number}
    headers = {'Content-Type': 'application/json'}
    
    response = requests.post(otp_url, json=payload, headers=headers)
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception("Failed to send OTP")

if __name__ == "__main__":
    phone_number = input("Enter phone number: ")
    try:
        result = send_otp(phone_number)
        print("OTP sent successfully:", result)
    except Exception as e:
        print("Error:", e)
