# Ex.05 Design a Website for Server Side Processing
# Date:
# AIM:
To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side.

# FORMULA:
P = I2R
P --> Power (in watts)
 I --> Intensity
 R --> Resistance

# DESIGN STEPS:
## Step 1:
Clone the repository from GitHub.

## Step 2:
Create Django Admin project.

## Step 3:
Create a New App under the Django Admin project.

## Step 4:
Create python programs for views and urls to perform server side processing.

## Step 5:
Create a HTML file to implement form based input and output.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
<div class="container">
    <h2>Lamp Filament Power Calculator</h2>
    <form id="calculator-form">
        <label for="intensity">Current Intensity (I) in Amperes:</label>
        <input type="number" id="intensity" placeholder="Enter intensity in amperes" step="any" required>

        <label for="resistance">Resistance (R) in Ohms:</label>
        <input type="number" id="resistance" placeholder="Enter resistance in ohms" step="any" required>

        <label for="power">Power (P) in Watts:</label>
        <input type="number" id="power" placeholder="Enter power in watts" step="any" disabled>

        <button type="button" onclick="calculatePower()">Calculate Power (P)</button>
    </form>

    <div class="result" id="result"></div>
    <div class="error" id="error"></div>
</div>

<script>
    function calculatePower() {
        const intensity = parseFloat(document.getElementById('intensity').value);
        const resistance = parseFloat(document.getElementById('resistance').value);
        const power = parseFloat(document.getElementById('power').value);
        document.getElementById('result').innerHTML = '';
        document.getElementById('error').innerHTML = '';
        if (isNaN(intensity) || isNaN(resistance) || intensity <= 0 || resistance <= 0) {
            document.getElementById('error').innerHTML = 'Please enter valid positive values for intensity and resistance.';
            return;
        }
        if (!isNaN(intensity) && !isNaN(resistance) && isNaN(power)) {
            const calculatedPower = Math.pow(intensity, 2) * resistance;
            document.getElementById('result').innerHTML = `Power (P) = ${calculatedPower.toFixed(2)} Watts`;
        }
        else if (!isNaN(intensity) && !isNaN(power) && isNaN(resistance)) {
            const calculatedResistance = power / Math.pow(intensity, 2);
            if (calculatedResistance <= 0) {
                document.getElementById('error').innerHTML = 'Calculated resistance should be positive.';
                return;
            }
            document.getElementById('result').innerHTML = `Resistance (R) = ${calculatedResistance.toFixed(2)} Ohms`;
        }
        else if (!isNaN(power) && !isNaN(resistance) && isNaN(intensity)) {
            const calculatedIntensity = Math.sqrt(power / resistance);
            if (calculatedIntensity <= 0) {
                document.getElementById('error').innerHTML = 'Calculated intensity should be positive.';
                return;
            }
            document.getElementById('result').innerHTML = `Current Intensity (I) = ${calculatedIntensity.toFixed(2)} Amperes`;
        } else {
            document.getElementById('error').innerHTML = 'Please leave one input empty for calculation.';
        }
    }
</script>
from django.shortcuts import render def lamp_calculator(request): intensity = None resistance = None power = None error_message = None if request.method == 'POST': try: intensity = float(request.POST.get('intensity', '')) resistance = float(request.POST.get('resistance', '')) power = float(request.POST.get('power', '')) if intensity and resistance: power = round(intensity**2 * resistance, 2) elif intensity and power: resistance = round(power / (intensity**2), 2) elif resistance and power: intensity = round((power / resistance)**0.5, 2) else: error_message = "Please enter at least two values." except ValueError: error_message = "Please enter valid numeric values." return render(request, 'lamp_calculator/index.html', { 'intensity': intensity, 'resistance': resistance, 'power': power, 'error_message': error_message, }) from django.urls import path from mathapp import views
urlpatterns = [ path('', views.lamp_calculator, name='lamp_calculator'),
]



#SERVER SIDE PROCESSING:
<img width="764" height="447" alt="image" src="https://github.com/user-attachments/assets/0fa0ae49-9056-4d4d-af1d-bd690cec492c" />


# HOMEPAGE:
<img width="775" height="484" alt="image" src="https://github.com/user-attachments/assets/f0a0aa30-76b1-49ee-bb8a-88d4e6781ad7" />


#RESULT:
The program for performing server side processing is completed successfully.
