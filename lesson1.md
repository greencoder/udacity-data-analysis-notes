# 6. Quiz: CSVs in Python

This is the original code as presented:

```
import unicodecsv

enrollments_filename = '/datasets/ud170/udacity-students/enrollments.csv'

## Longer version of code (replaced with shorter, equivalent version below)

# enrollments = []
# f = open(enrollments_filename, 'rb')
# reader = unicodecsv.DictReader(f)
# for row in reader:
#     enrollments.append(row)
# f.close()

with open(enrollments_filename, 'rb') as f:
    reader = unicodecsv.DictReader(f)
    enrollments = list(reader)
    
### Write code similar to the above to load the engagement
### and submission data. The data is stored in files with
### the given filenames. Then print the first row of each
### table to make sure that your code works. You can use the
### "Test Run" button to see the output of your code.

engagement_filename = '/datasets/ud170/udacity-students/daily_engagement.csv'
submissions_filename = '/datasets/ud170/udacity-students/project_submissions.csv'
    
daily_engagement = None     # Replace this with your code
project_submissions = None  # Replace this with your code
```

This is the accepted answer:

```
import unicodecsv

enrollments_filename = '/datasets/ud170/udacity-students/enrollments.csv'
engagement_filename = '/datasets/ud170/udacity-students/daily_engagement.csv'
submissions_filename = '/datasets/ud170/udacity-students/project_submissions.csv'

with open(enrollments_filename, 'rb') as f:
    reader = unicodecsv.DictReader(f)
    enrollments = list(reader)

with open(engagement_filename, 'rb') as f:
    reader = unicodecsv.DictReader(f)
    daily_engagement = list(reader)

with open(submissions_filename, 'rb') as f:
    reader = unicodecsv.DictReader(f)
    project_submissions = list(reader)

print daily_engagement[0]
print project_submissions[0]
```

# 9. Quiz: Investigating the Data

> For each of the three files you've loaded, find the total number of rows in the csv and the number of unique students. To find the number of unique students in each table, you might want to try creating a set of the account keys.

Here is the code as presented:

```
import unicodecsv

def read_csv(filename):
    with open(filename, 'rb') as f:
        reader = unicodecsv.DictReader(f)
        return list(reader)

enrollments = read_csv('/datasets/ud170/udacity-students/enrollments.csv')
daily_engagement = read_csv('/datasets/ud170/udacity-students/daily_engagement.csv')
project_submissions = read_csv('/datasets/ud170/udacity-students/project_submissions.csv')
    
### For each of these three tables, find the number of rows in the table and
### the number of unique students in the table. To find the number of unique
### students, you might want to create a set of the account keys in each table.

enrollment_num_rows = 0             # Replace this with your code
enrollment_num_unique_students = 0  # Replace this with your code

engagement_num_rows = 0             # Replace this with your code
engagement_num_unique_students = 0  # Replace this with your code

submission_num_rows = 0             # Replace this with your code
submission_num_unique_students = 0  # Replace this with your code
```

Here is the solution:

```
import unicodecsv

def read_csv(filename):
    with open(filename, 'rb') as f:
        reader = unicodecsv.DictReader(f)
        return list(reader)

enrollments = read_csv('/datasets/ud170/udacity-students/enrollments.csv')
daily_engagement = read_csv('/datasets/ud170/udacity-students/daily_engagement.csv')
project_submissions = read_csv('/datasets/ud170/udacity-students/project_submissions.csv')

enrollment_num_rows = len(enrollments)
enrollment_num_unique_students = len(set([e['account_key'] for e in enrollments]))

engagement_num_rows = len(daily_engagement)
engagement_num_unique_students = len(set([e['acct'] for e in daily_engagement]))

submission_num_rows = len(project_submissions)
submission_num_unique_students = len(set([e['account_key'] for e in project_submissions]))

# Note: This shorthand syntax is called a list comprehension:
# [e['account_key'] for e in enrollments]

# It is functionally equivilent to using a for loop, but it's more concise:
# enrollments = []
# for e in enrollments:
#     enrollments.append(e)

# To turn a list into a set, you can wrap the list in the set() function:
# unique_enrollments = set(enrollments)
```
