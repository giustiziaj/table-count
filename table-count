#!/usr/bin/env python3
# script to count records in each table in an sql database
import pymysql as mysql

def parse_arguments():
    from argparse import ArgumentParser
    import getpass as gp
    
    parser = ArgumentParser()

    parser.add_argument('-H', '--host',
                        help='connect to host.',
                        default='localhost',
                        type=str)
    parser.add_argument('-p', '--port',
                        help='port number to use for connection.',
                        default=3306,
                        type=int)
    parser.add_argument('-u', '--user',
                        help='username login if not the current user',
                        default=gp.getuser(),
                        type=str)
    parser.add_argument('-d', '--database',
                        help='database to connect.',
                        type=str)

    args = parser.parse_args()
    args.passwd = gp.getpass(prompt='Password for %s: ' % args.user)
    return args

### Main Thread ###
args = parse_arguments()
counts = {}

try:
    connection = mysql.connect(host=args.host,
                               user=args.user,
                               db=args.database,
                               port=args.port,
                               passwd=args.passwd)
except mysql.err.OperationalError:
    exit('Error: Incorrect Password')

try:
    crsr = connection.cursor()
    crsr.execute('show tables')
    tables = crsr.fetchall()
    for table in tables:
        crsr.execute('select count(*) from %s' % table[0])
        counts[table[0]] = crsr.fetchone()[0]

except Exception as err:
    exit('Error: %s' % str(err))
finally:
    connection.close()

for table in counts.keys():
    print('%s: %s' % (table, counts[table]))


