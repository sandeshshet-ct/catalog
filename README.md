# catalog
test 1

import json
import numpy as np

#### Sample JSON data as a string (this would typically be read from a file)
json_data = '''{
    "keys": {
        "n": 4,
        "k": 3
    },
    "1": {
        "base": "10",
        "value": "4"
    },
    "2": {
        "base": "2",
        "value": "111"
    },
    "3": {
        "base": "10",
        "value": "12"
    },
    "6": {
        "base": "4",
        "value": "213"
    }
}'''

##### Parse the JSON data
data = json.loads(json_data)

#### Function to decode values from different bases
def decode_value(base, value):
    return int(value, int(base))

#### Extracting roots
roots = []
for key in data.keys():
    if key.isdigit():  # Process only numeric keys
        base = data[key]['base']
        value = data[key]['value']
        x = int(key)  # x is the key
        y = decode_value(base, value)  # Decode y value
        roots.append((x, y))

#### Roots after decoding
print("Decoded Roots:", roots)

#### Split into x and y values for interpolation
x_values = [x for x, y in roots]
y_values = [y for x, y in roots]

#### Function to calculate polynomial coefficients using Lagrange interpolation
def lagrange_interpolation(x_values, y_values, x):
    total = 0
    for i in range(len(y_values)):
        product = y_values[i]
        for j in range(len(x_values)):
            if i != j:
                product *= (x - x_values[j]) / (x_values[i] - x_values[j])
        total += product
    return total

#### Calculate the constant term c (f(0)) of the polynomial
decoded_c = lagrange_interpolation(x_values, y_values, 0)
print("Constant term c:", decoded_c)



## Output
Decoded Roots: [(1, 4), (2, 7), (3, 12), (6, 39)]
Constant term c: 2.9999999999999982

=== Code Execution Successful ===
