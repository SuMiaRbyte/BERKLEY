# What Drives Used Car Prices?

## Project overview
This project analyzes about 426,000 used car listings (a sample of a larger Kaggle dataset) to identify what makes a used car more or less expensive, and to give dealers practical guidance on what to stock.

## Notebook
[used_cars_price_analysis.ipynb](used_cars_price_analysis.ipynb)

## Data and cleaning
- Removed duplicates and unusable columns (`id`, `VIN`, `region`, `size`, `model`).
- Removed unrealistic listings: price outside $500 to $100,000, odometer outside 100 to 300,000 miles, and model year before 1990. This left about 363,000 listings.
- Missing categories were labeled "unknown"; missing numbers were filled with the median.
- Created a vehicle `age` feature and modeled the log of price because prices are heavily skewed.

## Method
Compared Linear Regression, Ridge, and Lasso, tuned with 5-fold cross-validation and judged on a held-out test set. All three performed almost identically. Lasso was chosen as the best model (R² = 0.68, average error about $5,000).

## Key findings
1. **Age:** each additional year lowers price by about 6.3% (compounding), so a 10-year-old car is worth roughly half as much as an otherwise similar new one.
2. **Mileage:** each additional 10,000 miles lowers price by about 3.9%.
3. **Fuel:** diesel vehicles sell for about 89% more than comparable vehicles.
4. **Manufacturer:** Porsche, Tesla, Lexus, and Audi carry premiums. Fiat, Mercury, Saturn, Mitsubishi, and Kia sell at discounts.
5. **Vehicle type:** off-road vehicles, convertibles, and pickups carry premiums.
6. **Engine size:** each extra cylinder adds about 10%.
7. **Condition and title:** fair or salvage condition cuts price by about 47%; missing or rare title statuses cut it by about a third.
8. **Little effect:** state, transmission, and paint color.

## Recommendations for dealers
1. Favor newer, lower-mileage vehicles, since age and mileage are the strongest price signals.
2. Stock premium segments: diesel, pickups, convertibles, off-road vehicles, larger engines, and brands like Lexus and Audi.
3. Buy discounted brands (Fiat, Mercury, Saturn, Mitsubishi, Kia) only at a matching discount.
4. Verify title status, and avoid fair or salvage condition cars unless priced accordingly.
5. Don't pay extra for paint color or transmission.

## Limitations
- The typical prediction error is about $5,000, so results show broad price drivers, not exact prices for individual cars.
- These are listing prices, not final sale prices.
- Results show association, not cause, and reflect this one dataset, so they may differ by region or over time.
- Each effect is measured with the other factors held equal, so effects overlap in real cars (older cars usually have more miles) and should not be added together.
- Categories labeled "infrequent" combine rare values, so they cannot be read as one specific brand or title status.

## Next steps
- Add vehicle `model` to the analysis, since make and model likely explain more of the price.
- Track days-on-lot to link price to how fast cars sell.
- Refresh the analysis regularly with new data.

## Repository structure
```
├── data/
│   └── vehicles.csv
├── used_cars_price_analysis.ipynb
└── README.md
```

## Data source
The dataset is a used car listings sample from Kaggle (about 426,000 of the original 3 million records). If `vehicles.csv` is not included in this repo because of GitHub's file size limit, download it from the course materials or Kaggle and place it in the `data/` folder.
