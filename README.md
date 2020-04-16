# pytyvo_list


### Convertir de JSON a CSV

Para convertir los archivos JSON a CSV sin perder mucho tiempo, copiar y pegar este script en una terminal

```
mkdir pytyvo && cd pytyvo
wget https://raw.githubusercontent.com/gustavodbs/pytyvo_list/master/data/pdf{1,2,3}.json

python3 -m venv venv_pandas
source venv_pandas/bin/activate
pip install --upgrade pip
pip install pandas

cat<<EOF>convertir.py
#!/bin/env python3

import pandas
import sys


def convertir(archivo):
    print("Convirtiendo {0} -> {0}.csv".format(archivo))
    j = pandas.read_json(archivo)
    j.to_csv("{0}.csv".format(archivo))
    print("Ok")


def main():

    if len(sys.argv) < 2:
        print("Archivos JSON?")
        sys.exit()

    for archivo in sys.argv[1:]:
        convertir(archivo)


if __name__ == "__main__":
    main()

EOF

python convertir.py ./*.json

for f in *.csv ; do file $f ; done

zip todos_en_csv.zip ./*.csv
du -hc todos_en_csv.zip

```


