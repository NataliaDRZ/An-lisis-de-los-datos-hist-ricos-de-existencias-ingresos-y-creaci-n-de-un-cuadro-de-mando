# Análisis de los datos históricos de existencias-ingresos y creación de un cuadro de mando
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1>Extraer datos bursátiles usando la librería 'yfinance' de Python </h1>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Supongamos que trabajamos para una gestora de fondos de inversión; nuestro trabajo consistirá en determinar cualquier actividad de compra-venta de acciones para realizar un análisis posterior con los datos extraídos. En este laboratorio, extraeremos los datos de existencias mediante la biblioteca yfinance, que nos permitirá extraer de Yahoo finanzas datos e información de las acciones\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>Contenido</h2>\n",
    "<div class=\"alert alert-block alert-info\" style=\"margin-top: 20px\">\n",
    "    <ul>\n",
    "        <li>1 - Uso yfinance para extraer información de acciones</li>\n",
    "        <li>2 - Uso yfinance para extraer datos históricos de precios de acciones</li>\n",
    "        <li>3 - Uso de yfinance para extraer datos históricos de dividendos</li>\n",
    "        <li>4 - Ejercicio</li>\n",
    "    </ul>\n",
    "</div>\n",
    "\n",
    "<hr>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Instalamos la librería yfinance\n",
    "Esta librería permite descargar datos históricos económico financieros desde Yahoo Finanzas. Podremos acceder de un modo sencillo a una interesante gama de datos. Más información en https://pypi.org/project/yfinance/"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Collecting yfinance\n",
      "  Downloading yfinance-0.1.63.tar.gz (26 kB)\n",
      "Requirement already satisfied: pandas>=0.24 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from yfinance) (1.1.3)\n",
      "Requirement already satisfied: numpy>=1.15 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from yfinance) (1.19.2)\n",
      "Requirement already satisfied: requests>=2.20 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from yfinance) (2.24.0)\n",
      "Collecting multitasking>=0.0.7\n",
      "  Downloading multitasking-0.0.9.tar.gz (8.1 kB)\n",
      "Requirement already satisfied: lxml>=4.5.1 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from yfinance) (4.6.1)\n",
      "Requirement already satisfied: python-dateutil>=2.7.3 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from pandas>=0.24->yfinance) (2.8.1)\n",
      "Requirement already satisfied: pytz>=2017.2 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from pandas>=0.24->yfinance) (2020.1)\n",
      "Requirement already satisfied: chardet<4,>=3.0.2 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from requests>=2.20->yfinance) (3.0.4)\n",
      "Requirement already satisfied: certifi>=2017.4.17 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from requests>=2.20->yfinance) (2020.6.20)\n",
      "Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from requests>=2.20->yfinance) (1.25.11)\n",
      "Requirement already satisfied: idna<3,>=2.5 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from requests>=2.20->yfinance) (2.10)\n",
      "Requirement already satisfied: six>=1.5 in c:\\users\\mrsanchez\\anaconda3\\lib\\site-packages (from python-dateutil>=2.7.3->pandas>=0.24->yfinance) (1.15.0)\n",
      "Building wheels for collected packages: yfinance, multitasking\n",
      "  Building wheel for yfinance (setup.py): started\n",
      "  Building wheel for yfinance (setup.py): finished with status 'done'\n",
      "  Created wheel for yfinance: filename=yfinance-0.1.63-py2.py3-none-any.whl size=23914 sha256=00cfb7ca5adf87a773f2043f7c775b8cbd1f46fd7a909510934db16be79d6a1d\n",
      "  Stored in directory: c:\\users\\mrsanchez\\appdata\\local\\pip\\cache\\wheels\\ec\\cc\\c1\\32da8ee853d742d5d7cbd11ee04421222eb354672020b57297\n",
      "  Building wheel for multitasking (setup.py): started\n",
      "  Building wheel for multitasking (setup.py): finished with status 'done'\n",
      "  Created wheel for multitasking: filename=multitasking-0.0.9-py3-none-any.whl size=8372 sha256=6710745adb7b243b00c3493ad96e60e86be0d4c6e5ca2e27177fb014bb109092\n",
      "  Stored in directory: c:\\users\\mrsanchez\\appdata\\local\\pip\\cache\\wheels\\57\\6d\\a3\\a39b839cc75274d2acfb1c58bfead2f726c6577fe8c4723f13\n",
      "Successfully built yfinance multitasking\n",
      "Installing collected packages: multitasking, yfinance\n",
      "Successfully installed multitasking-0.0.9 yfinance-0.1.63\n"
     ]
    }
   ],
   "source": [
    "!pip install yfinance\n",
    "#!pip install pandas"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Importamos las librerías \"yfinance\" y \"pandas\" "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "import yfinance as yf\n",
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 1- Uso de la libreria yfinance para extraer datos de acciones\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Utilizando el método Ticker() podemos extraer información bursátil pasandole como parámetro las siglas identificativas de con las que a la empresa es identificada en la bolsa. Como ejemplo vamos a recuperar las acciones de la empresa Apple y cuyas siglas identificativas son AAPL.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "apple = yf.Ticker(\"AAPL\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Información de acciones\n",
    "Usando el atributo <code>info</code> podemos extraer información de las acciones de Apple en un diccionario de Python."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'zip': '95014',\n",
       " 'sector': 'Technology',\n",
       " 'fullTimeEmployees': 147000,\n",
       " 'longBusinessSummary': 'Apple Inc. designs, manufactures, and markets smartphones, personal computers, tablets, wearables, and accessories worldwide. It also sells various related services. The company offers iPhone, a line of smartphones; Mac, a line of personal computers; iPad, a line of multi-purpose tablets; and wearables, home, and accessories comprising AirPods, Apple TV, Apple Watch, Beats products, HomePod, iPod touch, and other Apple-branded and third-party accessories. It also provides AppleCare support services; cloud services store services; and operates various platforms, including the App Store, that allow customers to discover and download applications and digital content, such as books, music, video, games, and podcasts. In addition, the company offers various services, such as Apple Arcade, a game subscription service; Apple Music, which offers users a curated listening experience with on-demand radio stations; Apple News+, a subscription news and magazine service; Apple TV+, which offers exclusive original content; Apple Card, a co-branded credit card; and Apple Pay, a cashless payment service, as well as licenses its intellectual property. The company serves consumers, and small and mid-sized businesses; and the education, enterprise, and government markets. It sells and delivers third-party applications for its products through the App Store. The company also sells its products through its retail and online stores, and direct sales force; and third-party cellular network carriers, wholesalers, retailers, and resellers. Apple Inc. was founded in 1977 and is headquartered in Cupertino, California.',\n",
       " 'city': 'Cupertino',\n",
       " 'phone': '408-996-1010',\n",
       " 'state': 'CA',\n",
       " 'country': 'United States',\n",
       " 'companyOfficers': [],\n",
       " 'website': 'http://www.apple.com',\n",
       " 'maxAge': 1,\n",
       " 'address1': 'One Apple Park Way',\n",
       " 'industry': 'Consumer Electronics',\n",
       " 'ebitdaMargins': 0.31955,\n",
       " 'profitMargins': 0.25004,\n",
       " 'grossMargins': 0.41005,\n",
       " 'operatingCashflow': 104414003200,\n",
       " 'revenueGrowth': 0.364,\n",
       " 'operatingMargins': 0.28788,\n",
       " 'ebitda': 110934999040,\n",
       " 'targetLowPrice': 125,\n",
       " 'recommendationKey': 'buy',\n",
       " 'grossProfits': 104956000000,\n",
       " 'freeCashflow': 80625876992,\n",
       " 'targetMedianPrice': 160,\n",
       " 'currentPrice': 147.2,\n",
       " 'earningsGrowth': 1,\n",
       " 'currentRatio': 1.062,\n",
       " 'returnOnAssets': 0.19302,\n",
       " 'numberOfAnalystOpinions': 39,\n",
       " 'targetMeanPrice': 159.34,\n",
       " 'debtToEquity': 210.782,\n",
       " 'returnOnEquity': 1.27125,\n",
       " 'targetHighPrice': 185,\n",
       " 'totalCash': 61696000000,\n",
       " 'totalDebt': 135491002368,\n",
       " 'totalRevenue': 347155005440,\n",
       " 'totalCashPerShare': 3.732,\n",
       " 'financialCurrency': 'USD',\n",
       " 'revenuePerShare': 20.61,\n",
       " 'quickRatio': 0.887,\n",
       " 'recommendationMean': 2,\n",
       " 'exchange': 'NMS',\n",
       " 'shortName': 'Apple Inc.',\n",
       " 'longName': 'Apple Inc.',\n",
       " 'exchangeTimezoneName': 'America/New_York',\n",
       " 'exchangeTimezoneShortName': 'EDT',\n",
       " 'isEsgPopulated': False,\n",
       " 'gmtOffSetMilliseconds': '-14400000',\n",
       " 'quoteType': 'EQUITY',\n",
       " 'symbol': 'AAPL',\n",
       " 'messageBoardId': 'finmb_24937',\n",
       " 'market': 'us_market',\n",
       " 'annualHoldingsTurnover': None,\n",
       " 'enterpriseToRevenue': 7.21,\n",
       " 'beta3Year': None,\n",
       " 'enterpriseToEbitda': 22.562,\n",
       " '52WeekChange': 0.29013848,\n",
       " 'morningStarRiskRating': None,\n",
       " 'forwardEps': 5.34,\n",
       " 'revenueQuarterlyGrowth': None,\n",
       " 'sharesOutstanding': 16530199552,\n",
       " 'fundInceptionDate': None,\n",
       " 'annualReportExpenseRatio': None,\n",
       " 'totalAssets': None,\n",
       " 'bookValue': 3.882,\n",
       " 'sharesShort': 96355309,\n",
       " 'sharesPercentSharesOut': 0.0058,\n",
       " 'fundFamily': None,\n",
       " 'lastFiscalYearEnd': 1601078400,\n",
       " 'heldPercentInstitutions': 0.59102,\n",
       " 'netIncomeToCommon': 86801997824,\n",
       " 'trailingEps': 5.108,\n",
       " 'lastDividendValue': 0.22,\n",
       " 'SandP52WeekChange': 0.31455648,\n",
       " 'priceToBook': 37.9186,\n",
       " 'heldPercentInsiders': 0.00068999996,\n",
       " 'nextFiscalYearEnd': 1664150400,\n",
       " 'yield': None,\n",
       " 'mostRecentQuarter': 1624665600,\n",
       " 'shortRatio': 1.14,\n",
       " 'sharesShortPreviousMonthDate': 1623715200,\n",
       " 'floatShares': 16513139929,\n",
       " 'beta': 1.202797,\n",
       " 'enterpriseValue': 2502902939648,\n",
       " 'priceHint': 2,\n",
       " 'threeYearAverageReturn': None,\n",
       " 'lastSplitDate': 1598832000,\n",
       " 'lastSplitFactor': '4:1',\n",
       " 'legalType': None,\n",
       " 'lastDividendDate': 1620345600,\n",
       " 'morningStarOverallRating': None,\n",
       " 'earningsQuarterlyGrowth': 0.932,\n",
       " 'priceToSalesTrailing12Months': 7.0091033,\n",
       " 'dateShortInterest': 1626307200,\n",
       " 'pegRatio': 1.53,\n",
       " 'ytdReturn': None,\n",
       " 'forwardPE': 27.565542,\n",
       " 'lastCapGain': None,\n",
       " 'shortPercentOfFloat': 0.0058,\n",
       " 'sharesShortPriorMonth': 108937943,\n",
       " 'impliedSharesOutstanding': None,\n",
       " 'category': None,\n",
       " 'fiveYearAverageReturn': None,\n",
       " 'previousClose': 146.95,\n",
       " 'regularMarketOpen': 146.98,\n",
       " 'twoHundredDayAverage': 131.78065,\n",
       " 'trailingAnnualDividendYield': 0.005682205,\n",
       " 'payoutRatio': 0.16309999,\n",
       " 'volume24Hr': None,\n",
       " 'regularMarketDayHigh': 147.84,\n",
       " 'navPrice': None,\n",
       " 'averageDailyVolume10Day': 75906475,\n",
       " 'regularMarketPreviousClose': 146.95,\n",
       " 'fiftyDayAverage': 141.56372,\n",
       " 'trailingAnnualDividendRate': 0.835,\n",
       " 'open': 146.98,\n",
       " 'toCurrency': None,\n",
       " 'averageVolume10days': 75906475,\n",
       " 'expireDate': None,\n",
       " 'algorithm': None,\n",
       " 'dividendRate': 0.88,\n",
       " 'exDividendDate': 1628208000,\n",
       " 'circulatingSupply': None,\n",
       " 'startDate': None,\n",
       " 'regularMarketDayLow': 146.17,\n",
       " 'currency': 'USD',\n",
       " 'trailingPE': 28.817541,\n",
       " 'regularMarketVolume': 29498682,\n",
       " 'lastMarket': None,\n",
       " 'maxSupply': None,\n",
       " 'openInterest': None,\n",
       " 'marketCap': 2433245249536,\n",
       " 'volumeAllCurrencies': None,\n",
       " 'strikePrice': None,\n",
       " 'averageVolume': 81387312,\n",
       " 'dayLow': 146.17,\n",
       " 'ask': 147.21,\n",
       " 'askSize': 1400,\n",
       " 'volume': 29498682,\n",
       " 'fiftyTwoWeekHigh': 150,\n",
       " 'fromCurrency': None,\n",
       " 'fiveYearAvgDividendYield': 1.29,\n",
       " 'fiftyTwoWeekLow': 103.1,\n",
       " 'bid': 147.2,\n",
       " 'tradeable': False,\n",
       " 'dividendYield': 0.006,\n",
       " 'bidSize': 1300,\n",
       " 'dayHigh': 147.84,\n",
       " 'regularMarketPrice': 147.2,\n",
       " 'logo_url': 'https://logo.clearbit.com/apple.com'}"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "apple_info=apple.info\n",
    "apple_info #mostramos lo que tiene la variable"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Como ya tenemos un diccionario, podemos extraer la información a partir del campo clave. Extraemos por ejemplo el país mediante la clave <code>'country'</code>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'United States'"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "apple_info['country']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 2 - Uso yfinance para extraer datos históricos de precios de acciones\n",
    "Para realizar un análisis necesitamos extraer la evolución histórica de los indicadores principales (precio de apertura, máximo, mínimo, precio de cierre, etc.). Para ello usamos el método <code>history()</code>. Le podemos pasar como parámetro el periodo de tiempo cuyos datos queremos recoger. Las opciones para el período son 1 día (1d), 5d, 1 mes (1mo), 3mo, 6mo, 1 año (1y), 2y, 5y, 10y, ytd y max, este último (max) recoge el histórico completo desde la primera cotización en bolsa de la empresa."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "                  Open        High         Low       Close     Volume  \\\n",
      "Date                                                                    \n",
      "1980-12-12    0.100751    0.101189    0.100751    0.100751  469033600   \n",
      "1980-12-15    0.095933    0.095933    0.095495    0.095495  175884800   \n",
      "1980-12-16    0.088923    0.088923    0.088485    0.088485  105728000   \n",
      "1980-12-17    0.090676    0.091114    0.090676    0.090676   86441600   \n",
      "1980-12-18    0.093304    0.093742    0.093304    0.093304   73449600   \n",
      "...                ...         ...         ...         ...        ...   \n",
      "2021-07-30  144.380005  146.330002  144.110001  145.860001   70382000   \n",
      "2021-08-02  146.360001  146.949997  145.250000  145.520004   62880000   \n",
      "2021-08-03  145.809998  148.039993  145.179993  147.360001   64660800   \n",
      "2021-08-04  147.270004  147.789993  146.279999  146.949997   56319800   \n",
      "2021-08-05  146.979996  147.839996  146.169998  147.301498   31752985   \n",
      "\n",
      "            Dividends  Stock Splits  \n",
      "Date                                 \n",
      "1980-12-12        0.0           0.0  \n",
      "1980-12-15        0.0           0.0  \n",
      "1980-12-16        0.0           0.0  \n",
      "1980-12-17        0.0           0.0  \n",
      "1980-12-18        0.0           0.0  \n",
      "...               ...           ...  \n",
      "2021-07-30        0.0           0.0  \n",
      "2021-08-02        0.0           0.0  \n",
      "2021-08-03        0.0           0.0  \n",
      "2021-08-04        0.0           0.0  \n",
      "2021-08-05        0.0           0.0  \n",
      "\n",
      "[10249 rows x 7 columns]\n"
     ]
    }
   ],
   "source": [
    "historico_apple = apple.history(period=\"max\")\n",
    "print(historico_apple)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "El formato en el que se devuelven los datos es un DataFrame de Pandas. Con la 'Fecha' como índice, la acción 'Open', 'High', 'Low', 'Close', 'Volume' y 'Stock Splits' que se dan para cada día.\n",
    "Haciendo uso de los métodos <code>head()</code> y <code>tail()</code> podremos ver las primeras líneas o las ultimas respectivamente. Como parámetro se les pasa el número de líneas a visualizar, si no se le proporciona este parámetro por defecto muestra cinco líneas."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Open</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Dividends</th>\n",
       "      <th>Stock Splits</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>1980-12-12</th>\n",
       "      <td>0.100751</td>\n",
       "      <td>0.101189</td>\n",
       "      <td>0.100751</td>\n",
       "      <td>0.100751</td>\n",
       "      <td>469033600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-15</th>\n",
       "      <td>0.095933</td>\n",
       "      <td>0.095933</td>\n",
       "      <td>0.095495</td>\n",
       "      <td>0.095495</td>\n",
       "      <td>175884800</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-16</th>\n",
       "      <td>0.088923</td>\n",
       "      <td>0.088923</td>\n",
       "      <td>0.088485</td>\n",
       "      <td>0.088485</td>\n",
       "      <td>105728000</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-17</th>\n",
       "      <td>0.090676</td>\n",
       "      <td>0.091114</td>\n",
       "      <td>0.090676</td>\n",
       "      <td>0.090676</td>\n",
       "      <td>86441600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-18</th>\n",
       "      <td>0.093304</td>\n",
       "      <td>0.093742</td>\n",
       "      <td>0.093304</td>\n",
       "      <td>0.093304</td>\n",
       "      <td>73449600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                Open      High       Low     Close     Volume  Dividends  \\\n",
       "Date                                                                       \n",
       "1980-12-12  0.100751  0.101189  0.100751  0.100751  469033600        0.0   \n",
       "1980-12-15  0.095933  0.095933  0.095495  0.095495  175884800        0.0   \n",
       "1980-12-16  0.088923  0.088923  0.088485  0.088485  105728000        0.0   \n",
       "1980-12-17  0.090676  0.091114  0.090676  0.090676   86441600        0.0   \n",
       "1980-12-18  0.093304  0.093742  0.093304  0.093304   73449600        0.0   \n",
       "\n",
       "            Stock Splits  \n",
       "Date                      \n",
       "1980-12-12           0.0  \n",
       "1980-12-15           0.0  \n",
       "1980-12-16           0.0  \n",
       "1980-12-17           0.0  \n",
       "1980-12-18           0.0  "
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "historico_apple.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Si queremos mostrar los diez primero registros de los datos de una sola columna; por ejemplo la columna de precio de la acción al cierre de la jornada"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Date\n",
      "1980-12-12    0.100751\n",
      "1980-12-15    0.095495\n",
      "1980-12-16    0.088485\n",
      "1980-12-17    0.090676\n",
      "1980-12-18    0.093304\n",
      "1980-12-19    0.098999\n",
      "1980-12-22    0.103817\n",
      "1980-12-23    0.108198\n",
      "1980-12-24    0.113892\n",
      "1980-12-26    0.124405\n",
      "Name: Close, dtype: float64\n"
     ]
    }
   ],
   "source": [
    "print(historico_apple[\"Close\"].head(10))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Podemos restablecer el índice del DataFrame con la función reset_index. También establecemos el parámetro inplace en True para que el cambio tenga lugar en el propio DataFrame.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [],
   "source": [
    "historico_apple.reset_index(inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Graficamos el precio al cierre por fecha. Usamos el campo `Close` y el campo `Date`:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Date'>"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "historico_apple.plot(x=\"Date\", y=\"Close\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 3 - Uso de yfinance para extraer datos históricos de dividendos\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Los dividendos son la distribución de las ganancias de una empresa a los accionistas. En este caso, se definen como una cantidad de dinero devuelta por acción que posee un inversor. Usando la variable 'dividens' podemos obtener un DataFrame de los datos. El período de los datos viene dado por el período definido en la función \"history\".\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Date\n",
       "1987-05-11    0.000536\n",
       "1987-08-10    0.000536\n",
       "1987-11-17    0.000714\n",
       "1988-02-12    0.000714\n",
       "1988-05-16    0.000714\n",
       "                ...   \n",
       "2020-05-08    0.205000\n",
       "2020-08-07    0.205000\n",
       "2020-11-06    0.205000\n",
       "2021-02-05    0.205000\n",
       "2021-05-07    0.220000\n",
       "Name: Dividends, Length: 71, dtype: float64"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "apple.dividends"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Podemos graficar los dividendos a lo largo del tiempo:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Date'>"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "apple.dividends.plot()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 4- Ejercicio\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Con todo lo visto anteriormente, vamos a extraer los datos de una empresa española conocida, los mostramos y graficamos la evolución de los valores desde que empezó a cotizar en bolsa.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [],
   "source": [
    "inditex = yf.Ticker(\"ITX.MC\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Question 1</b> Mostramos el país de la empresa"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'Spain'"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "inditex_info=inditex.info\n",
    "inditex_info['country']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Question 2</b> Mostramos el sector al que pertenece\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'Consumer Cyclical'"
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "inditex_info['sector']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Question 3</b> Extraemos el histórico desde que empezó a cotizar en bolsa y lo graficamos"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "                 Open       High        Low      Close     Volume  Dividends  \\\n",
      "Date                                                                           \n",
      "2001-05-24  -0.137869  -0.138635  -0.134423  -0.138176  216270100        0.0   \n",
      "2001-05-25  -0.137869  -0.140780  -0.137103  -0.137946   50448300        0.0   \n",
      "2001-05-28  -0.136337  -0.138022  -0.135725  -0.137103   26118945        0.0   \n",
      "2001-05-29  -0.136414  -0.138865  -0.136414  -0.138405   26910070        0.0   \n",
      "2001-05-30  -0.138099  -0.139708  -0.137946  -0.138635   48229995        0.0   \n",
      "...               ...        ...        ...        ...        ...        ...   \n",
      "2021-07-30  28.500000  28.719999  28.270000  28.590000    2524564        0.0   \n",
      "2021-08-02  28.809999  29.530001  28.750000  29.100000   13035296        0.0   \n",
      "2021-08-03  29.129999  29.290001  28.730000  28.870001    1425722        0.0   \n",
      "2021-08-04  29.040001  29.049999  28.580000  28.650000    1260747        0.0   \n",
      "2021-08-05  28.690001  28.879999  28.549999  28.780001    1035664        0.0   \n",
      "\n",
      "            Stock Splits  \n",
      "Date                      \n",
      "2001-05-24           0.0  \n",
      "2001-05-25           0.0  \n",
      "2001-05-28           0.0  \n",
      "2001-05-29           0.0  \n",
      "2001-05-30           0.0  \n",
      "...                  ...  \n",
      "2021-07-30           0.0  \n",
      "2021-08-02           0.0  \n",
      "2021-08-03           0.0  \n",
      "2021-08-04           0.0  \n",
      "2021-08-05           0.0  \n",
      "\n",
      "[5137 rows x 7 columns]\n"
     ]
    }
   ],
   "source": [
    "historico_inditex=inditex.history(period=\"max\")\n",
    "print(historico_inditex)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {},
   "outputs": [],
   "source": [
    "historico_inditex.reset_index(inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Date'>"
      ]
     },
     "execution_count": 36,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "historico_inditex.plot(x=\"Date\", y=\"Close\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
