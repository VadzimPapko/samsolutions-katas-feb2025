# Business Analysis

In the context of validating tests for candidates, our current approach relies heavily on expert validation. This leads to high operational costs and scalability challenges as the number of candidates increases. This analysis explores the financial impact and presents the potential benefits of a more scalable solution.

## Assumptions

- **Test 1:**
    - Expert validation time per test: **3 hours**
- **Test 2:**
    - Expert validation time per test: **8 hours**
    - Amount of tokens to be processed: **20,000** (16,000 for input and 4,000 for output)
- **Candidate rate per hour:** $50
- **Software architecture licensing costs:** $800.00
- **Current available architectures:** 300

## Current Weekly Spendings

For 200 candidates:
(3 hours + 8 hours) × 200 candidates × \$50/hour = \$**110,000**


## Expert Availability and Requirements

- **Current availability per expert per week:** ~20 hours
- **Experts needed for N candidates:** `(11 × N) / 20`

## Scaling Analysis

| Candidates | Total Grading Hours | Experts Needed | Spending on Experts |
|------------|--------------------:|---------------:|--------------------:|
|        200 |              2,200h |            110 |          $220,000   |
|        500 |              5,500h |            275 |          $550,000   |
|      1,000 |             11,000h |            550 |        $1,100,000   |
|      1,500 |             16,500h |            825 |        $1,650,000   |
|      2,000 |             22,000h |          1,100 |        $2,200,000   |

**It is evident that managing 1,100 experts presents significant challenges in terms of hiring, onboarding, and retention.** One of our goals is to reduce the number of experts to improve scalability.

# LLM Solution Benefits

Implementing a Large Language Model (LLM) solution can address these challenges by:

- **Reducing Expert Dependency:** Automating the validation process decreases reliance on human experts.
- **Cost Efficiency:** Lower operational costs by minimizing expert hours.
- **Scalability:** Easily handle an increasing number of candidates without proportional increases in staffing.
- **Consistency:** Ensure uniform validation standards across all tests.

By integrating an LLM solution, we can streamline the validation process, making it more efficient and scalable while reducing costs and operational complexities.
# LLM Solution Benefits

## GPU Performance and Time per Case Calculations

The table below illustrates the processing capabilities of different NVIDIA A100 GPU configurations when handling candidate test cases.

| GPU Configuration | VRAM | Combined TPS (Tokens per Second) | Time per Case (seconds) | Time per 200 Cases (hours) | Time per 500 Cases (hours) | Time per 1000 Cases (hours) | Time per 1500 Cases (hours) | Time per 2000 Cases (hours) |
|-------------------|------|-------------------------------:|------------------------:|---------------------------:|---------------------------:|----------------------------:|----------------------------:|----------------------------:|
| 8x A100           | 320GB| 844.8                          | 23.67                   | 1.32                       | 3.29                       | 6.58                        | 9.86                        | 13.15                       |
| 2x A100           | 80GB | 211.2                          | 94.70                   | 5.26                       | 13.15                      | 26.30                       | 39.46                       | 52.61                       |
| 1x A100           | 40GB | 120.0                          | 166.67                  | 9.26                       | 23.15                      | 46.30                       | 69.44                       | 92.59                       |

*Assumptions: Each test case involves processing 20,000 tokens (16,000 input + 4,000 output).*

**Note:** The combined TPS for multiple GPUs assumes an 88% efficiency gain per additional GPU due to potential communication overhead.

## Comparative Analysis: Current Scenario vs. LLM Implementation

### Current Process Cost and Time Analysis

| Number of Candidates | Total Time Required (hours) | Total Cost ($) |
|----------------------|----------------------------:|---------------:|
| 200                  | 2,200                       | 110,000        |
| 500                  | 5,500                       | 275,000        |
| 1,000                | 11,000                      | 550,000        |
| 1,500                | 16,500                      | 825,000        |
| 2,000                | 22,000                      | 1,100,000      |

*Assumptions: Each candidate requires 11 hours of expert validation (3 hours for Test 1 and 8 hours for Test 2) at a rate of $50 per hour.*

### LLM-Assisted Process Cost and Time Analysis

**Positive Case Scenario:**

| Number of Candidates | Total Time Required (hours) | Total Cost ($) |
|----------------------|----------------------------:|---------------:|
| 200                  | 710                         | 35,500         |
| 500                  | 1,775                       | 88,750         |
| 1,000                | 3,550                       | 177,500        |
| 1,500                | 5,325                       | 266,250        |
| 2,000                | 7,100                       | 355,000        |

*Assumptions: Test 1 time reduced to 0.05 hours; Test 2 time reduced to 3.5 hours.*

**Worst Case Scenario:**

| Number of Candidates | Total Time Required (hours) | Total Cost ($) |
|----------------------|----------------------------:|---------------:|
| 200                  | 1,100                       | 55,000         |
| 500                  | 2,750                       | 137,500        |
| 1,000                | 5,500                       | 275,000        |
| 1,500                | 8,250                       | 412,500        |
| 2,000                | 11,000                      | 550,000        |

*Assumptions: Test 1 time reduced to 0.5 hours; Test 2 time reduced to 5 hours.*

## Potential Savings with LLM Implementation

| Number of Candidates | Time Saved per Week (hours) | Cost Savings ($) |
|----------------------|----------------------------:|-----------------:|
| 2,000                | 14,900                      | 745,000          |

*Based on the positive case scenario.*

## System Information

- **Model:** microsoft/phi-4 with 14 billion parameters.
- **Average Speed on A100 40GB GPU:** Approximately 120 tokens per second.

*Note:* Performance metrics are based on available data and may vary depending on specific configurations and workloads.

# On-Prem vs IaaS vs SaaS: Strategic Cost and Risk Analysis

When evaluating solutions for our infrastructure, we compared **On-Prem**, **IaaS**, and **SaaS** models, focusing on cost efficiency, scalability, and risk management.

Although an **On-Prem** solution initially appeared attractive, deeper analysis revealed significant challenges and hidden costs. In contrast, **IaaS** offered a balanced, flexible approach, while **SaaS** posed risks related to data privacy and vendor lock-in.

---

# Conclusion

Based on the comprehensive analysis above, we selected **IaaS on Microsoft Azure** using the **8x NVIDIA A100 HM on Phi-4** as the optimal solution for our infrastructure needs. This strategic choice delivers a significant improvement in scalability and processing power, enabling us to tackle challenges that were previously insurmountable with our existing setup.

### Key Advantages:
- **Scalability and Flexibility**: The 8x A100 configuration allows us to efficiently scale up or down based on workload demands, optimizing cost without compromising performance.
- **Time Efficiency**: Dramatic reduction in processing time compared to other alternatives, ensuring faster delivery and enhanced productivity.
- **Cost-Effectiveness**: Although slightly more expensive than lower-tier options, the time saved and improved operational efficiency justify the investment.

### Performance Scenarios:

#### Positive Scenario
Utilizing **8x NVIDIA A100 HM**, we achieve the following efficiency:

| Number of Tests | Time per Test (h) | Total Time Required (h) | Experts Needed |
|----------------:|------------------:|------------------------:|---------------:|
|             200 |              3.55 |                   710.0 |             36 |
|             500 |              3.55 |                 1,775.0 |             89 |
|           1,000 |              3.55 |                 3,550.0 |            178 |
|           1,500 |              3.55 |                 5,325.0 |            267 |
|           2,000 |              3.55 |                 7,100.0 |            355 |

#### Worst Case Scenario

Even under the most demanding conditions, this solution outperforms alternatives:

| Number of Tests | Time per Test (h) | Total Time Required (h) | Experts Needed |
|----------------:|------------------:|------------------------:|---------------:|
|             200 |               5.5 |                 1,100.0 |             55 |
|             500 |               5.5 |                 2,750.0 |            138 |
|           1,000 |               5.5 |                 5,500.0 |            275 |
|           1,500 |               5.5 |                 8,250.0 |            413 |
|           2,000 |               5.5 |                11,000.0 |            550 |

## Profit Calculation:
### Including Spendings on IaaS

For 2,000 candidates:
- **Total Savings**: $745,000
- **IaaS Spendings** (8x A100 at $358 per 13 hours):
  - $358 × (2,000 / 2,000) = \$358
- **Net Profit**:
  - \$745,000 - \$358 = **$744,642**

Therefore, by leveraging the LLM solution with the IaaS infrastructure, we achieve a net profit of **$744,642** for processing 2,000 candidates.

### Final Justification:
- **Time and Cost Efficiency**: The **8x A100 HM** enables us to complete complex processing tasks significantly faster, reducing total operational hours.
- **Operational Scalability**: This solution scales effectively with our increasing workload demands, minimizing bottlenecks and maximizing throughput.
- **Risk Mitigation**: Leveraging Azure's robust infrastructure reduces risks associated with hardware failures and maintenance challenges.

### Strategic Impact:
Adopting **IaaS with Microsoft Azure's 8x NVIDIA A100 HM** not only enhances our operational efficiency but also provides a strategic advantage by enabling rapid scaling and reducing time-to-market. This investment aligns with our long-term vision of cost-effective, high-performance computing.

This decision ensures that our infrastructure remains future-proof, adaptable, and capable of meeting the growing demands of our solutions, ultimately driving better outcomes and value for our stakeholders.