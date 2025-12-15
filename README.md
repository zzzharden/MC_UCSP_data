# School Scheduling Dataset for Guangxi Minzu University's School of Artificial Intelligence

## Overview
This dataset simulates the course scheduling scenario of the School of Artificial Intelligence at Guangxi Minzu University. It is generated to support research and development of course timetabling systems, including but not limited to timetable optimization, resource allocation, and constraint satisfaction problems. The dataset contains synthetic but realistic data on campuses, teachers, courses, classes, classrooms, and their relationships, designed to reflect actual academic scheduling requirements.


## Dataset Generation Process
The dataset is generated using a random data generation algorithm implemented in `data_generator.py`. The key generation steps are as follows:

1. **Campus Creation**: Generate multiple campuses with unique identifiers.
2. **Class Allocation**: Distribute classes proportionally across campuses, ensuring each campus has a reasonable number of classes.
3. **Teacher Generation**: Create teacher profiles with:
   - Randomly assigned primary campuses
   - A subset of multi-campus teachers (able to teach across multiple campuses)
   - Availability constraints (unavailable time slots)
   - Preferences for teaching days and periods
4. **Course Generation**: Generate courses with:
   - Four types: Theory (LT), Programming Lab (PL), Experiment Lab (EL), and Physical Training (PT)
   - Type-specific time preferences (e.g., PT prefers afternoon slots)
5. **Classroom Generation**: Create classrooms per campus with:
   - Types matching course requirements (CR for LT, LC for PL, etc.)
   - Capacity levels (S: Small, M: Medium, L: Large)
   - Specialized facilities (e.g., playgrounds for PT)
6. **Course Task Creation**: Generate teaching tasks by:
   - Assigning teachers to courses based on campus availability
   - Defining weekly hours, total hours, and session distributions
   - Setting constraints (e.g., PT cannot be scheduled in the last period of any day)
   - Assigning colors for visualization purposes
7. **Commute Time Setting**: Add commute times for multi-campus teachers between their assigned campuses.


## Dataset Structure
Each instance is stored as an Excel file with 6 worksheets, detailed below:

| Worksheet Name    | Description                                                                 | Key Columns                                                                 |
|-------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `TASK`            | Contains all course teaching tasks                                         | TASK_ID, TEACHER, COURSE, CTYPE (course type), WEEKLY_HOURS, TOTAL_HOURS, CLASSES, CAMPUS, START_W (start week), END_W (end week) |
| `TEACHER`         | Teacher information and constraints                                        | TEACHER (ID), CAMPUSES (assigned campuses), U_TIME (unavailable time slots), DAY_PREF (day preferences), PERIOD_PREF (period preferences) |
| `CLASS`           | Class-campus mapping                                                       | CLASS (ID), CAMPUS                                                          |
| `CLASSROOM`       | Classroom details                                                           | ROOM (ID), CAP (capacity), CTYPE (classroom type), CAMPUS, TEMP (temporary flag) |
| `COURSE`          | Course information and preferences                                         | COURSE (ID), CTYPE (course type), PERIOD_PREF (period preferences)          |
| `TEACHER_COMMUTE` | Commute times for multi-campus teachers                                     | TEACHER, CAMPUS, COMMUTE_TIME (minutes)                                     |


## Instance Variations
The dataset includes 20 instances with varying scales to support different research needs. Instances differ by:
- Number of campuses (2 to 6)
- Number of teachers (60 to 300)
- Number of course tasks (100 to 500)
- Number of classes (40 to 200)
- Number of multi-campus teachers (6 to 30)


## Usage
1. Download the desired instance files from the `data/` directory
2. Load the Excel files using spreadsheet software or programming libraries (e.g., `pandas` in Python)
3. Use the data for timetable optimization, constraint analysis, or algorithm development

Example Python code to load a dataset:
```python
import pandas as pd

# Load a specific instance
instance_id = 1
df_task = pd.read_excel(f'data/school_scheduling_instance_{instance_id}.xlsx', sheet_name='TASK')
df_teacher = pd.read_excel(f'data/school_scheduling_instance_{instance_id}.xlsx', sheet_name='TEACHER')

# Display basic information
print(f"Loaded instance {instance_id} with {len(df_task)} tasks and {len(df_teacher)} teachers")
```


## License
This dataset is released under the [MIT License](LICENSE).


## Acknowledgments
Generated based on the course scheduling requirements of the School of Artificial Intelligence at Guangxi Minzu University. For research purposes only.
