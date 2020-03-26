# UNIT-08_Learning_Journal
Unit 08 Learning Journal re-submission
"""
UNIT_08_Learning_Journal re-submission

This Python program does the following :
1. Creates a new file to disk called namebook
2. Reads this file into a dictionary
3. Inverts the dictionary
4. Writes to the output  file >>> phonebook.txt

Summary :
The original dictionary is written as a string consisting of the NAME of the contact person, with a list of PHONE numbers appended separated by VERTICAL BAR (pipe) as a delimiters.
The output file, phonebook.txt is subsequently written with a list of PHONE number and Contact name pairs.
"""

nbook = dict()

nbook ['Dick Tracy'] = ('90011001', '90011002', '90011003')

nbook ['Magnum PI'] = ('90012001', '90012002')

nbook ['Sherlock Holmes'] = ('90013001', '90013002', '90013003')

#  add 3 new terms to the dictionary

nbook ['John Lennon'] = ('90014001', '90014002', '90014003')

nbook ['Paul McCartney'] = ('90015001', '90015002')

nbook ['George Harrison'] = ('90016001', '90016002', '90016003')

# this dictionary takes input from namebook.txt"""

nb = {}

# this is the inverted phonebook

pbook = {}

#--------------------------------------------------------------------------------
#  Read from nbook and create the namebook.txt file
#--------------------------------------------------------------------------------

def write_namebook():

    with open ('namebook.txt', 'w') as wf:
         for k in nbook:
             line = (k + '|')
             for item in nbook[k]:
                 line = line + str(item) + '|'
             line = line + '\n'
             wf.write (line)

#  this routine inverts a dictionary


def invert_dict(book):

    newbook = dict()
    for key in book:
        for item in book[key]:
            newbook[item] = key
    return newbook

#--------------------------------------------------------------------------------
# read namebook.txt and write to nb dictionary
#--------------------------------------------------------------------------------

def write_phonebook():

    global pbook
    global nb

    with open ('namebook.txt', 'r') as rf:
         for line in rf:
             words = line.split('|')
             nlist = []
             phone = ''
             lcount = 0
             for word in words:
                 word = word.strip('\n')
                 lcount += 1
                 if lcount == 1:
                    phone = word
                 elif word != '':
                    nlist.append(word)
                    
             nb[phone] = nlist

#  convert nb to pbook dictionary

    pbook = invert_dict(nb)

#  write pbook to phonebook.txt file

    with open ('phonebook.txt', 'w') as wf:
         for k in pbook:
             nline = k + '|' + pbook[k] + '\n'
             wf.write (nline)

#--------------------------------------------------------------------------------
#  Main routine
#--------------------------------------------------------------------------------

def main():
           
    write_namebook()      # creates the namebook.txt file
    write_phonebook()     # creates the inverted phonebook.txt file

main()

#---------------------- e n d   o f   p r o g r a m -----------------------------

# The original file, namebook.txt is as foolows :

"""
Dick Tracy|90011001|90011002|90011003|
Magnum PI|90012001|90012002|
Sherlock Holmes|90013001|90013002|90013003|
John Lennon|90014001|90014002|90014003|
Paul McCartney|90015001|90015002|
George Harrison|90016001|90016002|90016003|
"""

# The converted file, phonebook.txt is as follows :

"""
90011001|Dick Tracy
90011002|Dick Tracy
90011003|Dick Tracy
90012001|Magnum PI
90012002|Magnum PI
90013001|Sherlock Holmes
90013002|Sherlock Holmes
90013003|Sherlock Holmes
90014001|John Lennon
90014002|John Lennon
90014003|John Lennon
90015001|Paul McCartney
90015002|Paul McCartney
90016001|George Harrison
90016002|George Harrison
90016003|George Harrison
"""
