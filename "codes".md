CODES: 
>BASED ON TRANSPORTATION
# Define emission factors (kg CO₂ per mile)
emission_factors = {
    'car_gasoline': 0.411,
    'car_electric': 0.1,
    'bus': 0.056,
    'train': 0.041,
    'bicycle': 0.0,
    'walking': 0.0
}

# Function to calculate the transportation carbon footprint
def calculate_transportation_footprint(data):
    total_emissions = 0.0

    for mode, details in data.items():
        distance = details['distance']  # miles per trip
        frequency = details['frequency']  # trips per week

        # Calculate emissions for this mode
        emissions = distance * frequency * emission_factors.get(mode, 0)
        total_emissions += emissions

        print(f"{mode.capitalize()} emissions: {emissions:.2f} kg CO₂ per week")

    return total_emissions

# Sample user data
user_data = {
    'car_gasoline': {'distance': 15, 'frequency': 5},  # 15 miles per trip, 5 trips per week
    'bus': {'distance': 10, 'frequency': 3},           # 10 miles per trip, 3 trips per week
    'bicycle': {'distance': 2, 'frequency': 7}         # 2 miles per trip, 7 trips per week
}

# Calculate the user's weekly transportation carbon footprint
total_footprint = calculate_transportation_footprint(user_data)
print(f"\nTotal Transportation Carbon Footprint: {total_footprint:.2f} kg CO₂ per week")

>BASED ON DIGITAL/ENERGY USAGE

# Define emission factor for electricity (in kg CO₂ per kWh)
electricity_emission_factor = 0.92  # kg CO₂ per kWh

# Typical power consumption (in watts) for common digital devices
device_power_consumption = {
    'laptop': 50,      # watts
    'desktop': 150,    # watts
    'smartphone': 5,   # watts
    'tv': 100          # watts
}

# Function to calculate carbon footprint from home energy use
def calculate_home_energy_footprint(kwh_per_month):
    # Total emissions from electricity use at home
    emissions = kwh_per_month * electricity_emission_factor
    print(f"Home Energy Use Emissions: {emissions:.2f} kg CO₂ per month")
    return emissions

# Function to calculate carbon footprint from digital habits
def calculate_digital_habits_footprint(data):
    total_emissions = 0.0

    for device, usage in data.items():
        # Convert power usage to kWh (power in watts * hours per day * days per month) / 1000
        daily_kwh = (device_power_consumption[device] * usage['hours_per_day'] * 30) / 1000
        device_emissions = daily_kwh * electricity_emission_factor
        total_emissions += device_emissions

        print(f"{device.capitalize()} emissions: {device_emissions:.2f} kg CO₂ per month")

    return total_emissions

# Sample user data for electricity consumption and digital device usage
user_data = {
    'home_energy_kwh_per_month': 400,  # kWh consumed per month at home
    'digital_habits': {
        'laptop': {'hours_per_day': 5},     # hours used per day
        'desktop': {'hours_per_day': 2},
        'smartphone': {'hours_per_day': 4},
        'tv': {'hours_per_day': 3}
    }
}

# Calculate the user's carbon footprint from home energy use
home_energy_emissions = calculate_home_energy_footprint(user_data['home_energy_kwh_per_month'])

# Calculate the user's carbon footprint from digital habits
digital_habits_emissions = calculate_digital_habits_footprint(user_data['digital_habits'])

# Total carbon footprint from both home energy and digital habits
total_emissions = home_energy_emissions + digital_habits_emissions
print(f"\nTotal Carbon Footprint from Energy Use at Home and Digital Habits: {total_emissions:.2f} kg CO₂ per month")

>BASED ON SHOPPING DIET CONSUMER

# Emission factors for shopping items (kg CO₂ per item)
shopping_emission_factors = {
    'electronics': 100,
    'clothing': 20,
    'groceries': 2,
    'household_items': 10
}

# Emission factors for dietary choices (kg CO₂ per kg of food)
diet_emission_factors = {
    'red_meat': 27,
    'poultry': 6.9,
    'dairy': 3.2,
    'vegetables': 2,
    'grains': 1.1
}

# Function to calculate carbon footprint from shopping habits
def calculate_shopping_footprint(data):
    total_emissions = 0.0

    for item, details in data.items():
        quantity = details['quantity']  # Number of items purchased
        emissions = quantity * shopping_emission_factors.get(item, 0)
        total_emissions += emissions

        print(f"{item.capitalize()} emissions: {emissions:.2f} kg CO₂ per month")

    return total_emissions

# Function to calculate carbon footprint from dietary habits
def calculate_dietary_footprint(data):
    total_emissions = 0.0

    for food, details in data.items():
        quantity = details['kg_per_week']  # kg of food consumed per week
        emissions = quantity * diet_emission_factors.get(food, 0) * 4  # Monthly footprint
        total_emissions += emissions

        print(f"{food.capitalize()} emissions: {emissions:.2f} kg CO₂ per month")

    return total_emissions

# Sample user data for shopping and dietary habits
user_data = {
    'shopping_choices': {
        'electronics': {'quantity': 1},    # 1 electronic item per month
        'clothing': {'quantity': 3},       # 3 clothing items per month
        'groceries': {'quantity': 20},     # 20 grocery items per month
        'household_items': {'quantity': 5} # 5 household items per month
    },
    'dietary_habits': {
        'red_meat': {'kg_per_week': 0.5},  # 0.5 kg of red meat per week
        'poultry': {'kg_per_week': 1.0},   # 1 kg of poultry per week
        'dairy': {'kg_per_week': 1.5},     # 1.5 kg of dairy per week
        'vegetables': {'kg_per_week': 3.0},# 3 kg of vegetables per week
        'grains': {'kg_per_week': 2.0}     # 2 kg of grains per week
    }
}

# Calculate the user's carbon footprint from shopping choices
shopping_emissions = calculate_shopping_footprint(user_data['shopping_choices'])

# Calculate the user's carbon footprint from dietary habits
dietary_emissions = calculate_dietary_footprint(user_data['dietary_habits'])

# Total carbon footprint from both shopping and dietary habits
total_emissions = shopping_emissions + dietary_emissions
print(f"\nTotal Carbon Footprint from Shopping and Dietary Habits: {total_emissions:.2f} kg CO₂ per month")
