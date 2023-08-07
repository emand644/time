# time
def add_time(start, duration, day=None):
    days_of_week = ["monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday"]

    start_time, period = start.split()
    start_hour, start_minute = map(int, start_time.split(":"))

    duration_hour, duration_minute = map(int, duration.split(":"))

    total_minutes = start_hour * 60 + start_minute + duration_hour * 60 + duration_minute

    days_later = total_minutes // (24 * 60)
    remaining_minutes = total_minutes % (24 * 60)

    new_hour = remaining_minutes // 60
    new_minute = remaining_minutes % 60

    new_period = period
    if new_hour >= 12:
        new_period = "PM" if period == "AM" else "AM"
    if new_hour == 0:
        new_hour = 12
    elif new_hour > 12:
        new_hour -= 12

    result = f"{new_hour}:{new_minute:02d} {new_period}"

    if day:
        day = day.lower()
        day_index = days_of_week.index(day)
        new_day_index = (day_index + days_later) % 7
        new_day = days_of_week[new_day_index]
        result += f", {new_day.capitalize()}"

    if days_later == 1:
        result += " (next day)"
    elif days_later > 1:
        result += f" ({days_later} days later)"

    return result

# Test cases
print(add_time("3:00 PM", "3:10"))
print(add_time("11:30 AM", "2:32", "Monday"))
print(add_time("11:43 AM", "00:20"))
print(add_time("10:10 PM", "3:30"))
print(add_time("11:43 PM", "24:20", "tueSday"))
print(add_time("6:30 PM", "205:12"))
