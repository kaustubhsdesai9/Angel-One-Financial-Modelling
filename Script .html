-- 1. Create a simple table to hold the financial data
CREATE TABLE angel_one_financials (
    fiscal_year DATE,
    sales DECIMAL(10,2),
    operating_profit DECIMAL(10,2),
    net_profit DECIMAL(10,2),
    cash_from_ops DECIMAL(10,2),
    cash_from_investing DECIMAL(10,2),
    cash_from_financing DECIMAL(10,2)
)
;

-- 2. Insert the actual data from your Excel file
INSERT INTO angel_one_financials VALUES ('2016-03-31', 451.2, 443.34, 31.72, -77.44, -13.21, 39.59);
INSERT INTO angel_one_financials VALUES ('2017-03-31', 440.05, 397.94, 31.01, -209.97, -49.52, 350.33);
INSERT INTO angel_one_financials VALUES ('2018-03-31', 770.25, 529.86, 107.93, -309.49, 47.41, 238.89);
INSERT INTO angel_one_financials VALUES ('2019-03-31', 777.69, 470.41, 79.83, 689.44, -5.71, -360.9);
INSERT INTO angel_one_financials VALUES ('2020-03-31', 747.6, 671.83, 82.35, 643.3, -28.13, -448.89);
INSERT INTO angel_one_financials VALUES ('2021-03-31', 1288.69, 495.92, 296.86, -1198.67, 24.8, 894.12);
INSERT INTO angel_one_financials VALUES ('2022-03-31', 2291.9, 342.72, 624.81, 557.55, -52.35, -165.13);
INSERT INTO angel_one_financials VALUES ('2023-03-31', 3002.3, 274.67, 889.95, 804.2, -185.11, -908.13);
INSERT INTO angel_one_financials VALUES ('2024-03-31', 4272.34, 415.41, 1125.53, -329.9, -91.05, 1330.88);
INSERT INTO angel_one_financials VALUES ('2025-03-31', 5239.22, 529.24, 1172.08, -1859.84, -340.82, 1916.91);


WITH historical_trends AS (
    SELECT
        fiscal_year,
        sales,
        net_profit,
        cash_from_ops,
        
        -- Calculate Previous Year's Sales for Growth Formula
        LAG(sales) OVER (ORDER BY fiscal_year) as prev_year_sales,
        
        -- Calculate Previous Year's Cash for Trend
        LAG(cash_from_ops) OVER (ORDER BY fiscal_year) as prev_year_cash,
        
        -- Calculate Margins
        (net_profit / NULLIF(sales,0)) * 100 as net_profit_margin_pct,
        (cash_from_ops / NULLIF(sales,0)) * 100 as cash_flow_margin_pct
    FROM angel_one_financials
),
growth_stats AS (
    SELECT 
        *,
        -- YoY Growth Calculation
        ((sales - prev_year_sales) / NULLIF(prev_year_sales,0)) * 100 as yoy_sales_growth_pct
    FROM historical_trends
)
SELECT 
    fiscal_year,
    sales,
    yoy_sales_growth_pct,
    net_profit,
    net_profit_margin_pct,
    cash_from_ops,
    
    -- Question 6: Cash Conversion (Quality of Earnings)
    -- If > 1, company converts profit to cash well. If < 1, profit is "on paper".
    (cash_from_ops / NULLIF(net_profit,0)) as cash_conversion_ratio,

    -- Question 9: Simple Forecast for Next Year (Sales * 1.15)
    -- We assume a conservative 15% growth here. You can change 1.15 to your own assumption.
    sales * 1.15 as forecast_next_year_sales
    
FROM growth_stats
ORDER BY fiscal_year DESC
;




-- Question: What are the projected Sales and Cash Flows for the next 5 years (2026-2030) assuming revenue growth is capped at 15%?

WITH RECURSIVE 
-- 1. Get the Baseline Data (The latest year, 2025)
baseline AS (
    SELECT 
        fiscal_year,
        sales,
        cash_from_ops
    FROM angel_one_financials
    WHERE fiscal_year = '2025-03-31'
),

-- 2. Calculate Assumptions (Growth Rate & Margin)
assumptions AS (
    SELECT
        -- Calculate the raw CAGR first
        (POWER(
            (SELECT sales FROM angel_one_financials WHERE fiscal_year = '2025-03-31') / 
            NULLIF((SELECT sales FROM angel_one_financials WHERE fiscal_year = '2022-03-31'), 0), 
            1.0/3
        ) - 1) AS actual_cagr,
        
        -- Cap the Growth Rate at 15% using LEAST() function
        LEAST(
            0.15, 
            (POWER(
                (SELECT sales FROM angel_one_financials WHERE fiscal_year = '2025-03-31') / 
                NULLIF((SELECT sales FROM angel_one_financials WHERE fiscal_year = '2022-03-31'), 0), 
                1.0/3
            ) - 1)
        ) AS capped_growth_rate,

        -- Calculate 5-Year Average Cash Flow Margin
        (SELECT SUM(cash_from_ops) FROM angel_one_financials WHERE fiscal_year >= '2021-03-31') / 
        (SELECT SUM(sales) FROM angel_one_financials WHERE fiscal_year >= '2021-03-31') AS avg_cf_margin
),

-- 3. Recursive Projection (The Forecasting Engine)
projections AS (
    -- Base Case: Start with 2025 Actuals to project 2026
    SELECT 
        1 AS projection_year_index,
        DATE_ADD(fiscal_year, INTERVAL 1 YEAR) as forecast_date,
        sales * (1 + (SELECT capped_growth_rate FROM assumptions)) as projected_sales,
        (sales * (1 + (SELECT capped_growth_rate FROM assumptions))) * (SELECT avg_cf_margin FROM assumptions) as projected_cash_flow
    FROM baseline
    
    UNION ALL
    
    -- Recursive Step: Project subsequent years
    SELECT 
        projection_year_index + 1,
        DATE_ADD(forecast_date, INTERVAL 1 YEAR),
        projected_sales * (1 + (SELECT capped_growth_rate FROM assumptions)),
        (projected_sales * (1 + (SELECT capped_growth_rate FROM assumptions))) * (SELECT avg_cf_margin FROM assumptions)
    FROM projections
    WHERE projection_year_index < 5
)

-- 4. Final Report Output
SELECT 
    forecast_date as "Fiscal Year",
    ROUND(projected_sales, 2) as "Projected Revenue (Cr)",
    ROUND(projected_cash_flow, 2) as "Projected OCF (Cr)",
    CONCAT(ROUND((SELECT capped_growth_rate FROM assumptions) * 100, 1), '%') as "Growth Assumption",
    CONCAT(ROUND((SELECT avg_cf_margin FROM assumptions) * 100, 1), '%') as "Margin Assumption"
FROM projections;