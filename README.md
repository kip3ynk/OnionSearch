# OnionSearch
## Educational purposes only
[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)

OnionSearch is a Python3 script that scrapes urls on different ".onion" search engines. 

In 30 minutes you get thousands of unique urls.

## 💡 Prerequisite
[Python 3](https://www.python.org/download/releases/3.0/)
   
## 📚 Currently supported Search engines
- Ahmia
- TORCH (x2)
- Darksearch io
- OnionLand
- not Evil
- VisiTOR
- Dark Search Enginer
- Phobos
- Onion Search Server
- Grams (x2)
- Candle
- Tor Search Engine (x2)
- Torgle (x2)
- Onion Search Engine
- Tordex
- Tor66
- Tormax
- Haystack
- Multivac
- Evo Search
- Oneirun
- DeepLink

## 🛠️ Installation

```
git clone https://github.com/megadose/OnionSearch.git
cd OnionSearch
pip3 install -r requirements.txt
pip3 install 'urllib3[socks]'
python3 search.py -h
```

## 📈  Usage

Help:
```
usage: search.py [-h] [--proxy PROXY] [--output OUTPUT]
                 [--continuous_write CONTINUOUS_WRITE] [--limit LIMIT]
                 [--barmode BARMODE] [--engines [ENGINES [ENGINES ...]]]
                 [--exclude [EXCLUDE [EXCLUDE ...]]]
                 [--fields [FIELDS [FIELDS ...]]]
                 [--field_delimiter FIELD_DELIMITER]
                 search

positional arguments:
  search                The search string or phrase

optional arguments:
  -h, --help            show this help message and exit
  --proxy PROXY         Set Tor proxy (default: 127.0.0.1:9050)
  --output OUTPUT       Output File (default: output_$SEARCH_$DATE.txt), where $SEARCH is replaced by the first chars of the search string and $DATE is replaced by the datetime
  --continuous_write CONTINUOUS_WRITE
                        Write progressively to output file (default: False)
  --limit LIMIT         Set a max number of pages per engine to load
  --barmode BARMODE     Can be 'fixed' (default) or 'unknown'
  --engines [ENGINES [ENGINES ...]]
                        Engines to request (default: full list)
  --exclude [EXCLUDE [EXCLUDE ...]]
                        Engines to exclude (default: none)
  --fields [FIELDS [FIELDS ...]]
                        Fields to output to csv file (default: engine name link), available fields are shown below
  --field_delimiter FIELD_DELIMITER
                        Delimiter for the CSV fields

[...]
```

### Examples

To request all the engines for the word "computer":
```
python3 search.py "computer"
```

To request all the engines excepted "Ahmia" and "Candle" for the word "computer":
```
python3 search.py "computer" --exclude ahmia candle
```

To request only "Tor66", "DeepLink" and "Phobos" for the word "computer":
```
python3 search.py "computer" --engines tor66 deeplink phobos
```

The same as previously but limiting to 3 the number of pages to load per engine:
```
python3 search.py "computer" --engines tor66 deeplink phobos --limit 3
```

Please kindly note that the list of supported engines (and their keys) is given in the script help (-h).


### Output

#### Default output

By default, the file is written at the end of the process. The file will be csv formatted, containing the following columns:
```
"engine","name of the link","url"
```

#### Customizing the output fields

You can customize what will be flush in the output file by using the parameters `--fields` and `--field_delimiter`.

`--fields` allows you to add, remove, re-order the output fields. The default mode is show just below. Instead, you can for instance
choose to output:
```
"engine","name of the link","url","domain"
```
by setting `--fields engine name link domain`.

Or even, you can choose to output:
```
"engine","domain"
```
by setting `--fields engine domain`.

These are examples but there are many possibilities.

Finally, you can also choose to modify the CSV delimiter (comma by default), for instance: `--field_delimiter ";"`.

#### Changing filename

The filename will be set by default to `output_$DATE_$SEARCH.txt`, where $DATE represents the current datetime and $SEARCH the first
characters of the search string.

You can modify this filename by using `--output` when running the script, for instance:
```
python3 search.py "computer" --output "\$DATE.csv"
python3 search.py "computer" --output output.txt
python3 search.py "computer" --output "\$DATE_\$SEARCH.csv"
...
```
(Note that it might be necessary to escape the dollar character.)

In the csv file produced, the name and url strings are sanitized as much as possible, but there might still be some problems...

#### Write progressively

You can choose to progressively write to the output (instead of everything at the end, which would prevent
losing the results if something goes wrong). To do so you have to use `--continuous-write True`, just as is:
```
python3 search.py "computer" --continuous-write True
```
You can then use the `tail -f` (tail follow) Unix command to actively watch or monitor the results of the scraping.

## 📝 License
[GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.fr.html)


