# ### Energy-Optimizer

Creating a complete Python program for an Energy Optimizer requires several components, including data acquisition, analysis, and recommendation algorithms. Below is a simple yet illustrative example that outlines the basic structure and components of such a program. This example assumes you have access to a source of real-time energy consumption data, perhaps through an API or a simulated dataset.

```python
import random
import statistics
import datetime

class EnergyDataFetcher:
    """
    Simulates fetching real-time energy consumption data.
    In a real-world scenario, this would interface with an external API.
    """

    @staticmethod
    def fetch_data():
        # Simulated energy consumption data (kWh) for the past 24 hours
        return [random.uniform(0.5, 5.0) for _ in range(24)]  # Random values representing hourly consumption


class EnergyAnalyzer:
    """
    Analyzes energy consumption data to find patterns and anomalies.
    """

    def __init__(self, data):
        self.data = data

    def calculate_average_consumption(self):
        if not self.data:
            raise ValueError("Consumption data list is empty.")
        return statistics.mean(self.data)

    def find_peak_usage(self):
        if not self.data:
            raise ValueError("Consumption data list is empty.")
        peak_value = max(self.data)
        peak_hour = self.data.index(peak_value)
        return peak_hour, peak_value


class EnergyRecommendations:
    """
    Provides recommendations to optimize energy usage.
    """

    def __init__(self, average_consumption, peak_hour):
        self.average_consumption = average_consumption
        self.peak_hour = peak_hour

    def generate_recommendations(self):
        recommendations = []
        
        # Recommendation to reduce peak hour consumption
        recommendations.append(f"Try to reduce energy usage during peak hour at {self.peak_hour}:00.")

        # Recommendation to shift usage to off-peak hours for cost saving
        off_peak_hours = [hour for hour in range(24) if self.average_consumption > self.average_consumption * 0.8]
        recommendations.append(f"Consider shifting some usage to off-peak hours: {off_peak_hours}.")

        return recommendations


def main():
    try:
        # Fetch real-time energy consumption data
        data_fetcher = EnergyDataFetcher()
        consumption_data = data_fetcher.fetch_data()

        # Analyze the data
        analyzer = EnergyAnalyzer(consumption_data)
        average_consumption = analyzer.calculate_average_consumption()
        peak_hour, peak_usage = analyzer.find_peak_usage()

        # Display basic information
        print(f"Average Hourly Consumption: {average_consumption:.2f} kWh")
        print(f"Peak Usage at hour {peak_hour}: {peak_usage:.2f} kWh")

        # Generate and display recommendations
        recommendations = EnergyRecommendations(average_consumption, peak_hour)
        for rec in recommendations.generate_recommendations():
            print(f"Recommendation: {rec}")

    except ValueError as ve:
        print(f"Data error: {ve}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    main()
```

### Explanation:

1. **EnergyDataFetcher**: This class simulates fetching real-time energy consumption data. Replace this with real data acquisition logic in a practical scenario.

2. **EnergyAnalyzer**: It processes the fetched data to analyze average consumption and find peak usage hours. 

3. **EnergyRecommendations**: It uses the analysis to generate suggestions for optimizing energy consumption, like reducing usage during peak hours and shifting to off-peak times.

4. **Error Handling**: The program includes basic error handling for empty data and unexpected exceptions that may occur during execution.

5. **Random Data Generation**: Used for demonstration purposes; replace it with actual data collection methods in real-world use.

The code is structured to be easily extendable and modifiable as per the real-world requirements and additional data sources.