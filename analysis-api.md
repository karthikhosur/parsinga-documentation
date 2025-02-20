# Resume Analysis System Documentation

## Overview
The resume analysis system uses a sophisticated prompt-based approach to evaluate candidate resumes against job descriptions. The system employs Llama 3.1 to perform comprehensive analysis across multiple dimensions, providing detailed scoring and recommendations in a structured JSON format.

## Rating System

### General Rating Scale (0-100)
The system uses a granular 100-point scale divided into 20 distinct bands, each representing specific levels of domain expertise and role alignment:

| Score Range | Classification | Description |
|------------|----------------|-------------|
| 0-5 | Complete Mismatch | No relevant skills or experience |
| 6-10 | Irrelevant Domain | Different field, minimal transferable skills |
| 11-15 | Basic Transferable Skills | Different domain, some soft skills apply |
| 16-20 | Minor Skill Overlap | Few relevant technical skills, wrong domain |
| 21-25 | Some Transferable Experience | Related industry, wrong role |
| 26-30 | Broad Industry Match | Same sector, different function |
| 31-35 | Related Function | Similar role, different technical stack |
| 36-40 | Partial Technical Match | Some relevant technical skills |
| 41-45 | Foundation Match | Basic domain knowledge, needs training |
| 46-50 | Entry Level Domain Match | Junior level in correct domain |
| 51-55 | Developing Domain Experience | 1-2 years relevant experience |
| 56-60 | Intermediate Domain Fit | 2-3 years domain experience |
| 61-65 | Good Domain Background | 3-4 years relevant experience |
| 66-70 | Strong Domain Knowledge | 4-5 years domain expertise |
| 71-75 | Advanced Domain Expert | 5-6 years specific experience |
| 76-80 | Technical Domain Authority | 6-7 years domain mastery |
| 81-85 | Domain Leadership | 7-8 years + team leadership |
| 86-90 | Senior Domain Expert | 8-10 years domain excellence |
| 91-95 | Principal Level Match | 10+ years domain mastery |
| 96-100 | Distinguished Expert | Industry leader in domain |

## Scoring Components

### Domain Alignment Rules
The system enforces strict domain alignment requirements for scoring:
- Scores above 45 require core domain experience
- Scores above 60 require direct role experience
- Scores above 75 require industry-specific certifications
- Scores above 90 require leadership in the same domain

### Confidence Score Guidelines
Confidence scores indicate the reliability of the analysis:
- 90-100: High confidence with comprehensive domain-specific data
- 70-89: Good confidence with clear role alignment
- 50-69: Moderate confidence with some domain uncertainty
- Below 50: Low confidence with unclear domain match

### Calculation Weights

#### Overall Match Percentage
- Domain expertise: 40%
- Role-specific skills: 30%
- Industry experience: 20%
- Education alignment: 10%

#### Experience Match Score
- Domain relevance: 50%
- Role-specific experience: 30%
- Years in exact role: 20%

#### Skills Match Score
- Domain-specific skills: 50%
- Technical proficiency: 30%
- Soft skills relevance: 20%

## Proficiency Level Classifications

### Expert Level
Requirements:
- 7+ years in exact role
- Domain-specific certifications
- Leadership in same domain

### Advanced Level
Requirements:
- 4-6 years in exact role
- Recent domain experience
- Project ownership

### Intermediate Level
Requirements:
- 2-3 years in similar role
- Some domain exposure
- Team contribution

### Beginner Level
Characteristics:
- Less than 2 years experience
- No direct domain experience
- Basic understanding

## Cultural Fit Assessment
The system evaluates cultural fit based on:
- Domain-specific communication style
- Industry-standard practices
- Role-specific collaboration
- Domain leadership examples

## Priority Level Assignment
Candidates are assigned priority levels based on their match percentage:
- High: Domain expert with >75% match
- Medium: Related domain with 45-75% match
- Low: Different domain with <45% match

## Negative Match Indicators
The system flags these critical mismatches:
- No experience in required domain
- Missing critical technical skills
- Irrelevant industry background
- Misaligned career progression

## Data Handling Rules
For incomplete or unclear information:
- Numeric values: Use null
- String values: Use "unknown"
- Arrays: Use empty array []

## Output Structure
The analysis is returned in a structured JSON format with the following main sections:
1. Metadata
   - Data quality metrics
   - Data availability flags
2. Overall Analysis
   - Match percentage
   - Confidence score
   - Recommendations
   - Suitability scoring
   - Interview recommendations
3. Location Analysis
   - Candidate location details
   - Visa status
4. Skills Analysis
   - Matching skills with proficiency levels
   - Missing critical skills
   - Skill categorization
5. Experience Analysis
   - Relevant experience metrics
   - Industry alignment
   - Career progression
6. Education Analysis
   - Degree relevance
   - Certifications
   - Requirements assessment
7. Cultural Fit Analysis
   - Values alignment
   - Work style assessment
   - Team fit indicators

## JSON Field Descriptions

### Metadata Section
```json
{
    "metadata": {
        "data_quality": {
            "resume_completeness": "number 0-100",
            "job_description_completeness": "number 0-100",
            "overall_confidence": "number 0-100"
        },
        "data_availability": {
            "personal_info": "boolean",
            "contact_details": "boolean",
            "work_history": "boolean",
            "education": "boolean",
            "skills": "boolean",
            "location": "boolean"
        }
    }
}
```

#### Data Quality Fields
- `resume_completeness`: Measures how complete the resume is based on expected sections (contact info, work history, education, skills)
- `job_description_completeness`: Evaluates how well-defined the job requirements are
- `overall_confidence`: System's confidence in the analysis accuracy

#### Data Availability Fields
Boolean flags indicating presence of key information:
- `personal_info`: Basic candidate identification details
- `contact_details`: Contact information
- `work_history`: Employment history
- `education`: Educational background
- `skills`: Technical and soft skills
- `location`: Geographic information

### Overall Analysis Section
```json
{
    "overall_analysis": {
        "match_percentage": "number 0-100 or null",
        "confidence_score": "number 0-100",
        "recommendation": "string or unknown",
        "summary": "string or unknown",
        "suitability_score": {
            "role_alignment": "number 0-100 or null",
            "culture_fit": "number 0-100 or null",
            "growth_potential": "number 0-100 or null",
            "confidence_score": "number 0-100"
        },
        "interview_recommendation": {
            "should_interview": "boolean or null",
            "priority_level": "string: high|medium|low|unknown",
            "key_discussion_points": ["list of strings"],
            "confidence_score": "number 0-100"
        }
    }
}
```

#### Overall Analysis Fields
- `match_percentage`: Overall candidate fit considering all factors
- `confidence_score`: Confidence in the overall analysis
- `recommendation`: Clear hiring recommendation with justification
- `summary`: Key findings including red flags or concerns

#### Suitability Score Fields
- `role_alignment`: How well experience matches job requirements
- `culture_fit`: Alignment with company culture and values
- `growth_potential`: Assessment of career trajectory and learning ability
- `confidence_score`: Confidence in suitability assessment

#### Interview Recommendation Fields
- `should_interview`: Boolean recommendation for proceeding to interview
- `priority_level`: Urgency of interviewing the candidate
- `key_discussion_points`: Important topics to address in interview
- `confidence_score`: Confidence in interview recommendation

### Location Analysis Section
```json
{
    "location_analysis": {
        "confidence_score": "number 0-100",
        "candidate_location": {
            "current_location": {
                "city": "string or unknown",
                "state": "string or unknown",
                "country": "string or unknown",
                "time_zone": "string or unknown"
            },
            "visa_status": "string or unknown",
            "work_authorization": "string or unknown"
        }
    }
}
```

#### Location Analysis Fields
- `confidence_score`: Confidence in location information
- `current_location`: Detailed geographic information
- `visa_status`: Current visa or residency status
- `work_authorization`: Legal right to work status

### Skills Analysis Section
```json
{
    "skills_analysis": {
        "confidence_score": "number 0-100",
        "matching_skills": [{
            "skill": "string",
            "proficiency_level": "string: expert|advanced|intermediate|beginner|unknown",
            "years_of_experience": "number or null",
            "last_used": "string: YYYY or current or unknown",
            "confidence_score": "number 0-100",
            "relevance_to_role": "string: high|medium|low"
        }],
        "missing_critical_skills": ["list of strings"],
        "additional_relevant_skills": ["list of strings"],
        "skill_match_score": "number 0-100 or null",
        "technical_skills_rating": "number 0-100 or null",
        "soft_skills_rating": "number 0-100 or null",
        "skill_categorization": {
            "technical_skills": ["list of strings"],
            "soft_skills": ["list of strings"],
            "domain_knowledge": ["list of strings"],
            "tools_and_technologies": ["list of strings"]
        }
    }
}
```

#### Skills Analysis Fields
- `matching_skills`: Detailed analysis of skills matching job requirements
  - `skill`: Specific skill name
  - `proficiency_level`: Expertise level
  - `years_of_experience`: Years of using the skill
  - `last_used`: Most recent application of skill
  - `confidence_score`: Confidence in skill assessment
  - `relevance_to_role`: Importance to job requirements
- `missing_critical_skills`: Required skills not found in resume
- `additional_relevant_skills`: Valuable skills beyond requirements
- `skill_match_score`: Overall skills alignment score
- `technical_skills_rating`: Technical capabilities score
- `soft_skills_rating`: Non-technical capabilities score
- `skill_categorization`: Skills grouped by category

### Experience Analysis Section
```json
{
    "experience_analysis": {
        "confidence_score": "number 0-100",
        "years_of_experience": "number or null",
        "relevant_experience_years": "number or null",
        "experience_match_score": "number 0-100 or null",
        "relevant_positions": [{
            "title": "string or unknown",
            "company": "string or unknown",
            "duration": "string or unknown",
            "relevance_score": "number 0-100 or null",
            "key_responsibilities": ["list of strings"],
            "achievements": ["list of strings"],
            "data_completeness": {
                "has_dates": "boolean",
                "has_responsibilities": "boolean",
                "has_achievements": "boolean"
            }
        }],
        "industry_alignment": {
            "current_industry": "string or unknown",
            "target_industry": "string or unknown",
            "transition_feasibility": "number 0-100 or null",
            "transferable_skills": ["list of strings"]
        },
        "career_progression": {
            "trajectory": "string: upward|stable|varied|downward|unknown",
            "leadership_experience": "boolean or null",
            "management_experience_years": "number or null"
        }
    }
}
```

#### Experience Analysis Fields
- `years_of_experience`: Total work experience
- `relevant_experience_years`: Experience in related roles
- `experience_match_score`: Overall experience fit score
- `relevant_positions`: Detailed analysis of each relevant position
  - `relevance_score`: Position's relevance to job
  - `key_responsibilities`: Main duties
  - `achievements`: Notable accomplishments
  - `data_completeness`: Information completeness check
- `industry_alignment`: Industry experience analysis
  - `transition_feasibility`: Ease of industry switch
  - `transferable_skills`: Skills applicable to new industry
- `career_progression`: Career growth analysis
  - `trajectory`: Career direction
  - `leadership_experience`: Management history
  - `management_experience_years`: Years in leadership

### Education Analysis Section
```json
{
    "education_analysis": {
        "confidence_score": "number 0-100",
        "education_match_score": "number 0-100 or null",
        "degrees": [{
            "degree": "string or unknown",
            "field": "string or unknown",
            "institution": "string or unknown",
            "year": "string or unknown",
            "relevance_score": "number 0-100 or null"
        }],
        "certifications": [{
            "name": "string or unknown",
            "issuer": "string or unknown",
            "year": "string or unknown",
            "expiry": "string or null",
            "relevance_score": "number 0-100 or null"
        }],
        "meets_requirements": "boolean or null"
    }
}
```

#### Education Analysis Fields
- `education_match_score`: Overall education fit score
- `degrees`: Analysis of each degree
  - `relevance_score`: Degree's relevance to role
- `certifications`: Professional certifications
  - `relevance_score`: Certification's relevance to role
- `meets_requirements`: Educational requirements check

### Cultural Fit Analysis Section
```json
{
    "cultural_fit_analysis": {
        "confidence_score": "number 0-100",
        "values_alignment": "number 0-100 or null",
        "communication_style": "string or unknown",
        "work_style_preferences": ["list of strings"],
        "team_fit_indicators": ["list of strings"]
    }
}
```

#### Cultural Fit Analysis Fields
- `values_alignment`: Match with company values
- `communication_style`: Communication approach
- `work_style_preferences`: Working style indicators
- `team_fit_indicators`: Team compatibility factors

## Additional Features
- Executive Summary Generation (Optional)
- Timestamp Recording
- Error Handling for Invalid JSON
- HTTP Exception Management
- Authentication Token Support
