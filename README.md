import pandas
import csv 

with open('./fwdexetersecondroundofassessmentreg_/TranslateWords Challenge/french_dictionary.csv','rt')as f:
    data = csv.reader(f)
    r=[]
    for row in data:
        r.append(row)

filename = "./fwdexetersecondroundofassessmentreg_/TranslateWords Challenge/frequency.csv"
fields = ['English word','French word','Frequency'] 
# print (r)

# writing to csv file 
with open(filename, 'w', newline='') as csvfile: 
    # creating a csv writer object 
    csvwriter = csv.writer(csvfile) 
        
    # writing the fields 
    csvwriter.writerow(fields) 

    # writing the data rows 
    csvwriter.writerows(r)

df_state = pandas.read_csv('./fwdexetersecondroundofassessmentreg_/TranslateWords Challenge/frequency.csv')
# print(df_state)

df_duplicates = df_state[df_state.duplicated('French word')]['French word']
print(df_duplicates)
