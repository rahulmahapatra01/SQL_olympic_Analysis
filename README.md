<!DOCTYPE html>
<html lang="en">
<body>

<h1>🏅 Olympic Data Analysis with SQL</h1>
<p><strong>Project by:</strong> Rahul Mahapatra</p>
<p><strong>Domain:</strong> Sports Analytics | SQL</p>

<div class="section">
  <h2>📌 Project Overview</h2>
  <p>Analyzed 120+ years of Olympic Games data (1896–2020) using SQL to uncover:</p>
  <ul>
    <li>Medal trends (country performance, India’s Olympic journey)</li>
    <li>Athlete demographics (gender ratio, participation stats)</li>
    <li>Host city insights (USA’s Olympic hosting history)</li>
  </ul>
  <p><strong>Database:</strong> Olympic | <strong>Tools:</strong> MySQL</p>
</div>

<div class="section">
  <h2>🗃️ Database Schema</h2>
  <p><strong>Key Tables:</strong></p>
  <ul>
    <li><strong>Medal_Details:</strong> Tally of gold/silver/bronze by country.</li>
    <li><strong>Athlete_Bio:</strong> Athlete names, gender, and nationality.</li>
    <li><strong>Games_Held:</strong> Year, city, and host country for each edition.</li>
  </ul>
</div>

<div class="section">
  <h3>Sample Table Creation</h3>
  <pre><code>CREATE TABLE Medal_Details (
  edition VARCHAR(255),
  edition_id INT,
  year INT,
  country VARCHAR(255),
  country_noc VARCHAR(3),
  gold INT,
  silver INT,
  bronze INT,
  total INT,
  PRIMARY KEY (edition_id, country_noc)
);</code></pre>
</div>

<div class="section">
  <h2>🔍 SQL Queries & Insights</h2>

  <h3>Q1. Total Indian Athletes in Olympics</h3>
  <pre><code>SELECT COUNT(athlete_name) AS total_indian_athlete, country 
FROM athlete_bio 
WHERE country_noc = "IND" 
GROUP BY country;</code></pre>
  <p><strong>Insight:</strong> 1,035 athletes represented India exclusively.</p>

  <h3>Q2. Total Participating Countries</h3>
  <pre><code>SELECT COUNT(DISTINCT country_noc) AS total_country 
FROM country_details;</code></pre>
  <p><strong>Output:</strong> 234 countries participated.</p>

  <h3>Q3. India’s Medal Tally (All Time)</h3>
  <pre><code>SELECT SUM(gold) AS Gold, SUM(silver) AS Silver, 
       SUM(bronze) AS Bronze, SUM(total) AS Total 
FROM medal_details 
WHERE country = "India";</code></pre>
  <p><strong>Trend:</strong> India’s peak in 2012 (6 medals) and 2020 (7 medals).</p>

  <h3>Q4. Top 5 Countries by Gold Medals</h3>
  <pre><code>SELECT country, SUM(gold) AS gold_medals 
FROM medal_details 
GROUP BY country 
ORDER BY gold_medals DESC 
LIMIT 5;</code></pre>
  <p><strong>Insight:</strong> USA leads by a wide margin.</p>

  <h3>Q5. Highest Average Medals per Edition</h3>
  <pre><code>SELECT country, country_noc, AVG(total) AS avg_medals 
FROM medal_details 
GROUP BY country, country_noc 
ORDER BY avg_medals DESC 
LIMIT 5;</code></pre>
  <p><strong>Insight:</strong> Historical teams (EUN, URS) had high averages.</p>

  <h3>Q6. India’s Medal Trend Over Years</h3>
  <pre><code>SELECT year, SUM(total) AS total_medal 
FROM medal_details 
WHERE country_noc = 'IND' 
GROUP BY year;</code></pre>
  <p><strong>Key Years:</strong> 2020: 7 medals (Best performance), 1900–1950: Consistently 1–2 medals.</p>

  <h3>Q7. Male-to-Female Athlete Ratio</h3>
  <pre><code>SELECT 
  SUM(sex = 'male') AS male, 
  SUM(sex = 'female') AS female, 
  SUM(sex = 'male') / SUM(sex = 'female') AS ratio 
FROM athlete_bio;</code></pre>
  <p><strong>Issue:</strong> Gender disparity (~3:1 ratio).</p>

  <h3>Q8. Most Gold Medals in Football</h3>
  <pre><code>SELECT country, SUM(gold) AS total_gold 
FROM medal_details 
JOIN oly_results ON medal_details.edition_id = oly_results.edition_id 
WHERE sport = 'football' 
GROUP BY country 
ORDER BY total_gold DESC 
LIMIT 1;</code></pre>
  <p><strong>Winner:</strong> USA (948 golds in football).</p>

  <h3>Q9. USA’s Olympic Host Cities</h3>
  <pre><code>SELECT year, city 
FROM games_held 
WHERE country_noc = 'USA';</code></pre>
  <p><strong>Fact:</strong> LA hosted 3 times (1932, 1984, 2028).</p>

  <h3>Q10. 20th-Century Olympic Games</h3>
  <pre><code>SELECT * 
FROM games_held 
WHERE year BETWEEN 1900 AND 1999;</code></pre>
  <p><strong>Notable Editions:</strong> 1936 Berlin (Nazi propaganda), 1980 Lake Placid (Miracle on Ice).</p>
</div>

<div class="section">
  <h2>📊 Key Findings</h2>
  <ul>
    <li><strong>India’s Growth:</strong> Medal count surged post-2000 (peaked in 2020).</li>
    <li><strong>USA Dominance:</strong> Top in gold medals (1,195) and football.</li>
    <li><strong>Gender Gap:</strong> Male athletes outnumber females 2.86:1.</li>
    <li><strong>Host Cities:</strong> USA hosted 9 times (LA, Atlanta, Salt Lake City).</li>
  </ul>
</div>

</body>
</html>
