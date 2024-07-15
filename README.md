# moon-cicle
from datetime import datetime, timedelta

def moon_phase(year, month, day):
    # Algorithm by John Conway to calculate moon phase
    if month < 3:
        year -= 1
        month += 12

    month += 1

    K1 = int(365.25 * (year + 4712))
    K2 = int(30.6 * month + 0.5)
    K3 = int(int((year / 100) + 49) * 0.75) - 38

    JD = K1 + K2 + day + 59  # Julian date
    JD -= K3  # correction factor for the Gregorian calendar

    IP = (JD - 2451550.1) / 29.53058867  # Moon's age in days
    IP -= int(IP)  # remove the integer part of the result, leaving the fractional part

    age = IP * 29.53058867  # Convert fractional part to days

    if age < 1.84566:
        phase = "New Moon"
    elif age < 5.53699:
        phase = "Waxing Crescent"
    elif age < 9.22831:
        phase = "First Quarter"
    elif age < 12.91963:
        phase = "Waxing Gibbous"
    elif age < 16.61096:
        phase = "Full Moon"
    elif age < 20.30228:
        phase = "Waning Gibbous"
    elif age < 23.99361:
        phase = "Last Quarter"
    elif age < 27.68493:
        phase = "Waning Crescent"
    else:
        phase = "New Moon"

    return phase

# Get current date
today = datetime.now()
year = today.year
month = today.month
day = today.day

# Get moon phase for current date
current_moon_phase = moon_phase(year, month, day)
print(f"The current moon phase is: {current_moon_phase}")
