# Resume Analyzer Response Documentation

## Table of Contents
1. [Metadata](#metadata)
2. [Overall Analysis](#overall-analysis)
3. [Location Analysis](#location-analysis)
4. [Skills Analysis](#skills-analysis)
5. [Experience Analysis](#experience-analysis)
6. [Education Analysis](#education-analysis)
7. [Cultural Fit Analysis](#cultural-fit-analysis)

## Metadata

### Data Quality
- **resume_completeness** (number: 0-100)
  - Measures the completeness of essential resume components
  - Calculation factors:
    - Presence of contact information (15%)
    - Work history details (30%)
    - Education information (20%)
    - Skills section (25%)
    - Additional sections (10%)
  - Each section is weighted based on its importance
  - Missing sections reduce the score proportionally

- **job_description_completeness** (number: 0-100)
  - Evaluates the clarity and completeness of the job requirements
  - Calculation factors:
    - Role responsibilities (30%)
    - Required skills (25%)
    - Experience requirements (20%)
    - Education requirements (15%)
    - Company/team context (10%)

- **overall_confidence** (number: 0-100)
  - Aggregate measure of analysis reliability
  - Weighted average of:
    - Data quality scores (40%)
    - Data availability (30%)
    - Analysis depth (30%)

### Data Availability
Boolean flags indicating presence of key information:
- **personal_info**: Basic identification details
- **contact_details**: Contact information
- **work_history**: Employment records
- **education**: Educational background
- **skills**: Skills section
- **location**: Geographic information

## Overall Analysis

### Match Percentage (number: 0-100)
- Comprehensive fit score using weighted criteria:
  - Skills match (40%)
  - Experience relevance (30%)
  - Education alignment (20%)
  - Cultural fit (10%)
- Calculation process:
  1. Each component is scored independently
  2. Weights are applied
  3. Scores are normalized to 0-100 scale
  4. Final score is rounded to nearest integer

### Confidence Score (number: 0-100)
- Indicates reliability of match percentage
- Based on:
  - Data completeness (40%)
  - Information clarity (30%)
  - Analysis depth (30%)
- Score ranges:
  - 90-100: High confidence
  - 70-89: Good confidence
  - 50-69: Moderate confidence
  - Below 50: Low confidence

### Recommendation (string)
- Structured recommendation format:
  - Primary recommendation (Proceed/Consider/Decline)
  - Key justification points
  - Risk factors or concerns
  - Next steps
- Based on:
  - Match percentage thresholds
  - Critical requirements met/unmet
  - Red flags identified

### Suitability Score
- **role_alignment** (number: 0-100)
  - Measures direct experience match
  - Factors:
    - Years in similar roles (30%)
    - Relevant responsibilities (40%)
    - Industry experience (30%)

- **culture_fit** (number: 0-100)
  - Evaluates organizational culture alignment
  - Components:
    - Previous company cultures (30%)
    - Work style indicators (40%)
    - Values alignment (30%)

- **growth_potential** (number: 0-100)
  - Assesses candidate's development trajectory
  - Calculated from:
    - Learning agility indicators (35%)
    - Career progression (35%)
    - Skill development pattern (30%)

### Interview Recommendation
- **should_interview** (boolean)
  - Determined by:
    - Match percentage > 60%
    - No critical skill gaps
    - No major red flags

- **priority_level** (string: high|medium|low)
  - Based on match percentage:
    - High: > 80%
    - Medium: 60-80%
    - Low: < 60%

- **key_discussion_points** (array of strings)
  - Generated from:
    - Skill gaps
    - Experience clarifications
    - Potential concerns
    - Cultural fit aspects

## Location Analysis

### Candidate Location
- **current_location**
  - Extracted from resume contact information
  - Components:
    - city (string)
    - state (string)
    - country (string)
    - time_zone (string)

- **visa_status** (string)
  - Extracted from:
    - Explicit mentions
    - Work authorization statements
    - Citizenship information

- **work_authorization** (string)
  - Determined from:
    - Direct statements
    - Visa status
    - Geographic indicators

## Skills Analysis

### Matching Skills (array of objects)
Each skill object contains:
- **skill** (string)
  - Extracted through keyword matching
  - Normalized using skill taxonomy

- **proficiency_level** (string: expert|advanced|intermediate|beginner)
  - Determined by:
    - Years of experience
    - Context of usage
    - Project complexity
  - Classification criteria:
    - Expert: 8+ years, leadership experience
    - Advanced: 5-8 years, project ownership
    - Intermediate: 2-5 years, regular usage
    - Beginner: <2 years, basic application

- **years_of_experience** (number)
  - Calculated by:
    - Summing duration of roles using skill
    - Accounting for concurrent usage
    - Validating against timeline

- **last_used** (string: YYYY|current)
  - Based on:
    - Most recent role using skill
    - Project dates
    - Explicit mentions

- **confidence_score** (number: 0-100)
  - Reliability of skill assessment
  - Factors:
    - Information clarity
    - Context availability
    - Timeline consistency

- **relevance_to_role** (string: high|medium|low)
  - Determined by:
    - Job description emphasis
    - Skill importance
    - Application context

### Skill Categories
- **technical_skills** (array)
  - Hard skills
  - Technical competencies
  - Tool proficiencies

- **soft_skills** (array)
  - Interpersonal abilities
  - Leadership capabilities
  - Communication skills

- **domain_knowledge** (array)
  - Industry-specific expertise
  - Subject matter knowledge
  - Market understanding

- **tools_and_technologies** (array)
  - Software applications
  - Platforms
  - Technical tools

## Experience Analysis

### Experience Metrics
- **years_of_experience** (number)
  - Total professional experience
  - Calculated by:
    - Summing role durations
    - Handling overlaps
    - Excluding gaps

- **relevant_experience_years** (number)
  - Experience in related roles
  - Factors:
    - Similar responsibilities
    - Industry alignment
    - Skill application

### Relevant Positions (array of objects)
Each position contains:
- **title** (string)
- **company** (string)
- **duration** (string)
- **relevance_score** (number: 0-100)
  - Based on:
    - Role similarity (40%)
    - Skill overlap (30%)
    - Industry alignment (30%)

- **key_responsibilities** (array)
  - Extracted from:
    - Role descriptions
    - Achievement statements
    - Project details

- **achievements** (array)
  - Quantifiable results
  - Project outcomes
  - Recognition received

### Industry Alignment
- **current_industry** (string)
- **target_industry** (string)
- **transition_feasibility** (number: 0-100)
  - Assessed through:
    - Transferable skills
    - Industry overlap
    - Similar role types

### Career Progression
- **trajectory** (string: upward|stable|varied|downward)
  - Analyzed through:
    - Role progression
    - Responsibility growth
    - Title advancement

- **leadership_experience** (boolean)
  - Based on:
    - Management roles
    - Team leadership
    - Project oversight

## Education Analysis

### Degrees (array of objects)
Each degree contains:
- **degree** (string)
- **field** (string)
- **institution** (string)
- **year** (string)
- **relevance_score** (number: 0-100)
  - Calculated from:
    - Field alignment
    - Level appropriateness
    - Recent relevance

### Certifications (array of objects)
Each certification includes:
- **name** (string)
- **issuer** (string)
- **year** (string)
- **expiry** (string)
- **relevance_score** (number: 0-100)
  - Based on:
    - Role requirements
    - Industry standards
    - Current validity

## Cultural Fit Analysis

- **values_alignment** (number: 0-100)
  - Assessed through:
    - Achievement context
    - Work style indicators
    - Organizational values

- **communication_style** (string)
  - Analyzed from:
    - Resume language
    - Achievement descriptions
    - Role interactions

- **work_style_preferences** (array)
  - Identified through:
    - Role patterns
    - Achievement contexts
    - Team interactions

- **team_fit_indicators** (array)
  - Extracted from:
    - Collaboration examples
    - Team achievements
    - Leadership style

## Confidence Scoring Methodology

All confidence scores (0-100) follow this general framework:
- 90-100: High confidence
  - Comprehensive data
  - Clear evidence
  - Multiple confirmations

- 70-89: Good confidence
  - Substantial data
  - Minor gaps
  - Some inference needed

- 50-69: Moderate confidence
  - Partial data
  - Some uncertainty
  - Significant inference

- Below 50: Low confidence
  - Limited data
  - High uncertainty
  - Heavy inference needed

Confidence scores are calculated by evaluating:
1. Data completeness (40%)
2. Information clarity (30%)
3. Verification potential (30%)
