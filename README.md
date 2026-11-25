
India's Day Ahead Market: When Does the Price Ceiling Bind?

A 15 minute block level look at how often electricity prices in India’s Day Ahead Market hit the regulatory ceiling of ₹10/kWh, and what time of day it happens.

The Data

Source: Indian Energy Exchange (IEX), Day Ahead Market (DAM) Snapshot.
The market clears in 96 blocks of 15 minutes every day. This dataset covers 1 April 2024 to 22 November 2026, a total of 92,736 blocks across 966 days, with zero missing prices.
Because IEX caps exports at 31 days per download, I pulled the data month by month across 32 separate files and stacked them together. To my knowledge, this is the only public, continuous block level panel of the Indian DAM covering this timeframe.
The compiled dataset is saved as dam_clean.csv and is open for anyone to use with attribution.
• Columns: date, hour, block, purchase_bid, sell_bid, mcv, scheduled_vol, mcp (Market Clearing Price in ₹/MWh), blockno (1 to 96), month, year.

Methodology

The notebook dam_price_analysis.ipynb ingests the 32 raw files, strips out the summary rows at the bottom of each sheet, standardizes the dates, and converts prices to numeric values. Any block with a clearing price at or above ₹10,000/MWh (equivalent to ₹10/kWh) is flagged as capped. From there, the data is aggregated by day, block position, and year.
The ₹10/kWh ceiling has been in place since April 2023 and remained unchanged throughout this period, meaning none of these shifts are artifacts of a regulatory change.

Key Findings

1. Price capping has climbed sharply.
Through 2024 and 2025, roughly 10% to 25% of blocks cleared at the ceiling. That share surged through 2026, crossing 60% in September. On the tightest single day, 17 September 2026, 75 out of 96 blocks hit the ₹10 cap.
2. The ceiling only binds after sunset.
This was the most striking pattern in the data. Between blocks 41 and 66 (roughly 10:00 AM to 4:30 PM), prices hit the ceiling on 0% of days across every single year. Not rarely. Never. Abundant midday solar generation has made it structurally impossible for afternoon prices to touch the cap.
Once the sun goes down, the curve goes nearly vertical starting at block 68. By block 78 (around 7:15 PM), the 2026 curve hits the price ceiling on 68% of all days. In practice, the ceiling doesn't cap the overall market. It caps the evening peak.
3. The midday to evening price spread is widening.
Comparing average clearing prices (in ₹/MWh) across the midday solar window versus the evening peak shows a clear divergence:

Year	Midday Avg	Evening Avg	Spread	Ratio
2024	2,556	6,226	3,670	2.44
2025	2,094	6,313	4,219	3.02
2026	1,894	7,080	5,186	3.74

Midday prices have dropped every year while evening prices have climbed, widening the spread by 41% over 32 months. Daily medians follow the exact same trajectory, confirming this is a structural shift rather than a handful of outlier days skewing the mean.

Why This Matters

In 2026, the average evening price of ₹7,080/MWh already sits at 71% of the legal maximum, and the peak evening block is capped two days out of three. There is very little headroom left.
This creates a direct bottleneck for energy storage. Battery economics rely on the arbitrage spread between cheap charging hours and expensive discharging hours. Right now, solar is pushing midday charging costs down, while a regulatory ceiling is artificially compressing evening discharge revenues. Storage upside is being bounded by regulation rather than true market scarcity.
This is especially timely as the Central Electricity Regulatory Commission (CERC) actively reviews the ₹10 ceiling, following a petition from the National Solar Energy Federation of India (NSEFI) to raise or remove the cap on these exact grounds.

Caveats & Limitations

• IEX data only: Trading volumes from PXIL and HPX are not captured here.
• Standard DAM only: This excludes the High Price Day Ahead Market (HPDAM, which carries a ₹20/kWh ceiling) and the Real Time Market (RTM, which now accounts for roughly 42% of IEX volume). Because some evening demand spills into those segments, this shows that standard DAM was capped, not necessarily the entire power system.
• Theoretical spreads: The arbitrage table reflects raw price differences and does not account for round trip efficiency losses (~15%) or the operational reality that a battery cannot capture the entire window's average price.
• Descriptive, not causal: The spike in 2026 capping coincided with record power demand, a weak monsoon, lower hydro generation, and tightening coal stocks in autumn 2026. This analysis documents the market behavior without isolating those underlying drivers.

Figures

Tanisha Gandhi · tgandhi1@babson.edu · gandhitanisha36@gmail.com
