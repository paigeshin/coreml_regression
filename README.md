### Reference

https://developer.apple.com/documentation/createml/creating_a_model_from_tabular_data

https://towardsdatascience.com/mathematics-for-machine-learning-linear-regression-least-square-regression-de09cf53757c

### Regression

Regression is a method of modeling a `target` value based on independent predictors

### Price of House Example

- Sq feet
- Location
- Year
- Bedrooms
- Bathrooms
- Double story
- Pool

=> Actual Price of House

### Create mlmodel with Mac Playground

- You can always use `CreateML`

```swift
// macOS Playground

import Cocoa
import CoreML
import CreateML

let outputFileName = "/Users/paigeshin/Desktop/playground/regression/"

guard let csvFile = Bundle.main.url(forResource: "Mars", withExtension: "csv"),
    let dataTable = try? MLDataTable(contentsOf: csvFile) else {
        fatalError("Unable to load data!")
}

let regressorColumns = ["price", "solarPanels","greenhouses","size"]
let regressorTable = dataTable[regressorColumns]

let (regressorTestingTable, regressorTrainingTable) = regressorTable.randomSplit(by: 0.2)

let regressor = try MLLinearRegressor(trainingData: regressorTrainingTable, targetColumn: "price")

let metadata = MLModelMetadata(author: "Mohammad Azam", shortDescription: "Prediction of Martian Houses", version: "1.0")

try regressor.write(toFile: outputFileName, metadata: metadata)

```

### Code

```swift
    let model = LinearRegressor()
    guard let output = try? self.model.prediction(
        solarPanels: self.numberOfSolarPanels,
        greenhouses: self.numberOfGreenHouses,
        size: Int64(self.size) ?? 200
    ) else {
        return
    }

    self.predictedPrice = output.price < 0 ? "N/A" : "$\(output.price)"
```
