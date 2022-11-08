---
title: "First data analysis!"
date: 2022-11-08 15:51:25 -0400
categories: jekyll update
---

{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "17c60500",
   "metadata": {
    "_cell_guid": "b1076dfc-b9ad-4769-8c92-a6c4dae69d19",
    "_uuid": "8f2839f25d086af736a60e9eeb907d3b93b6e0e5",
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.054982Z",
     "iopub.status.busy": "2022-11-07T19:42:55.054370Z",
     "iopub.status.idle": "2022-11-07T19:42:55.069715Z",
     "shell.execute_reply": "2022-11-07T19:42:55.069071Z"
    },
    "papermill": {
     "duration": 0.028733,
     "end_time": "2022-11-07T19:42:55.072360",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.043627",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "/kaggle/input/french-bakery-daily-sales/Bakery sales.csv\n"
     ]
    }
   ],
   "source": [
    "# This Python 3 environment comes with many helpful analytics libraries installed\n",
    "# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python\n",
    "# For example, here's several helpful packages to load\n",
    "\n",
    "import numpy as np # linear algebra\n",
    "import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)\n",
    "\n",
    "# Input data files are available in the read-only \"../input/\" directory\n",
    "# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory\n",
    "\n",
    "import os\n",
    "for dirname, _, filenames in os.walk('/kaggle/input'):\n",
    "    for filename in filenames:\n",
    "        print(os.path.join(dirname, filename))\n",
    "\n",
    "# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using \"Save & Run All\" \n",
    "# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "853ea94b",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.091466Z",
     "iopub.status.busy": "2022-11-07T19:42:55.090492Z",
     "iopub.status.idle": "2022-11-07T19:42:55.095285Z",
     "shell.execute_reply": "2022-11-07T19:42:55.094371Z"
    },
    "papermill": {
     "duration": 0.016084,
     "end_time": "2022-11-07T19:42:55.097308",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.081224",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "d9796da0",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.115834Z",
     "iopub.status.busy": "2022-11-07T19:42:55.115480Z",
     "iopub.status.idle": "2022-11-07T19:42:55.488820Z",
     "shell.execute_reply": "2022-11-07T19:42:55.488161Z"
    },
    "papermill": {
     "duration": 0.385094,
     "end_time": "2022-11-07T19:42:55.491009",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.105915",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "df = pd.read_csv('/kaggle/input/french-bakery-daily-sales/Bakery sales.csv')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c519c82e",
   "metadata": {
    "papermill": {
     "duration": 0.008203,
     "end_time": "2022-11-07T19:42:55.508937",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.500734",
     "status": "completed"
    },
    "tags": []
   },
   "source": [
    "#### Not all of the columns are relevant, such as the ticket number, and time in minutes"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "bd8502b9",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.527452Z",
     "iopub.status.busy": "2022-11-07T19:42:55.526955Z",
     "iopub.status.idle": "2022-11-07T19:42:55.546932Z",
     "shell.execute_reply": "2022-11-07T19:42:55.546126Z"
    },
    "papermill": {
     "duration": 0.031282,
     "end_time": "2022-11-07T19:42:55.548732",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.517450",
     "status": "completed"
    },
    "tags": []
   },
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
       "      <th>Unnamed: 0</th>\n",
       "      <th>date</th>\n",
       "      <th>time</th>\n",
       "      <th>ticket_number</th>\n",
       "      <th>article</th>\n",
       "      <th>Quantity</th>\n",
       "      <th>unit_price</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>08:38</td>\n",
       "      <td>150040.0</td>\n",
       "      <td>BAGUETTE</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0,90 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1</td>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>08:38</td>\n",
       "      <td>150040.0</td>\n",
       "      <td>PAIN AU CHOCOLAT</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1,20 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>4</td>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>09:14</td>\n",
       "      <td>150041.0</td>\n",
       "      <td>PAIN AU CHOCOLAT</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1,20 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>5</td>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>09:14</td>\n",
       "      <td>150041.0</td>\n",
       "      <td>PAIN</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1,15 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>8</td>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>09:25</td>\n",
       "      <td>150042.0</td>\n",
       "      <td>TRADITIONAL BAGUETTE</td>\n",
       "      <td>5.0</td>\n",
       "      <td>1,20 €</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Unnamed: 0        date   time  ticket_number               article  \\\n",
       "0           0  2021-01-02  08:38       150040.0              BAGUETTE   \n",
       "1           1  2021-01-02  08:38       150040.0      PAIN AU CHOCOLAT   \n",
       "2           4  2021-01-02  09:14       150041.0      PAIN AU CHOCOLAT   \n",
       "3           5  2021-01-02  09:14       150041.0                  PAIN   \n",
       "4           8  2021-01-02  09:25       150042.0  TRADITIONAL BAGUETTE   \n",
       "\n",
       "   Quantity unit_price  \n",
       "0       1.0     0,90 €  \n",
       "1       3.0     1,20 €  \n",
       "2       2.0     1,20 €  \n",
       "3       1.0     1,15 €  \n",
       "4       5.0     1,20 €  "
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "9e17862c",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.566825Z",
     "iopub.status.busy": "2022-11-07T19:42:55.566430Z",
     "iopub.status.idle": "2022-11-07T19:42:55.580982Z",
     "shell.execute_reply": "2022-11-07T19:42:55.580213Z"
    },
    "papermill": {
     "duration": 0.025415,
     "end_time": "2022-11-07T19:42:55.582806",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.557391",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "df = df[['date','article','Quantity','unit_price']]"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e088ef93",
   "metadata": {
    "papermill": {
     "duration": 0.008128,
     "end_time": "2022-11-07T19:42:55.599481",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.591353",
     "status": "completed"
    },
    "tags": []
   },
   "source": [
    "#### Renaming the columns to make it more convenient"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "2cfc85b4",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.617183Z",
     "iopub.status.busy": "2022-11-07T19:42:55.616768Z",
     "iopub.status.idle": "2022-11-07T19:42:55.628769Z",
     "shell.execute_reply": "2022-11-07T19:42:55.628252Z"
    },
    "papermill": {
     "duration": 0.02295,
     "end_time": "2022-11-07T19:42:55.630649",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.607699",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "df = df.rename(columns={'unit_price': 'price', 'Quantity': 'quantity'})"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "38a471e4",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.649579Z",
     "iopub.status.busy": "2022-11-07T19:42:55.649223Z",
     "iopub.status.idle": "2022-11-07T19:42:55.660038Z",
     "shell.execute_reply": "2022-11-07T19:42:55.659206Z"
    },
    "papermill": {
     "duration": 0.022571,
     "end_time": "2022-11-07T19:42:55.662052",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.639481",
     "status": "completed"
    },
    "tags": []
   },
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
       "      <th>date</th>\n",
       "      <th>article</th>\n",
       "      <th>quantity</th>\n",
       "      <th>price</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>BAGUETTE</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0,90 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>PAIN AU CHOCOLAT</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1,20 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>PAIN AU CHOCOLAT</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1,20 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>PAIN</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1,15 €</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>TRADITIONAL BAGUETTE</td>\n",
       "      <td>5.0</td>\n",
       "      <td>1,20 €</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         date               article  quantity   price\n",
       "0  2021-01-02              BAGUETTE       1.0  0,90 €\n",
       "1  2021-01-02      PAIN AU CHOCOLAT       3.0  1,20 €\n",
       "2  2021-01-02      PAIN AU CHOCOLAT       2.0  1,20 €\n",
       "3  2021-01-02                  PAIN       1.0  1,15 €\n",
       "4  2021-01-02  TRADITIONAL BAGUETTE       5.0  1,20 €"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "3cba40f0",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.681277Z",
     "iopub.status.busy": "2022-11-07T19:42:55.680716Z",
     "iopub.status.idle": "2022-11-07T19:42:55.703744Z",
     "shell.execute_reply": "2022-11-07T19:42:55.702794Z"
    },
    "papermill": {
     "duration": 0.03466,
     "end_time": "2022-11-07T19:42:55.705609",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.670949",
     "status": "completed"
    },
    "tags": []
   },
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
       "      <th>quantity</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>234005.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>1.538377</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>1.289603</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>-200.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>200.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "            quantity\n",
       "count  234005.000000\n",
       "mean        1.538377\n",
       "std         1.289603\n",
       "min      -200.000000\n",
       "25%         1.000000\n",
       "50%         1.000000\n",
       "75%         2.000000\n",
       "max       200.000000"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "79358866",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.724755Z",
     "iopub.status.busy": "2022-11-07T19:42:55.724449Z",
     "iopub.status.idle": "2022-11-07T19:42:55.730872Z",
     "shell.execute_reply": "2022-11-07T19:42:55.730042Z"
    },
    "papermill": {
     "duration": 0.018034,
     "end_time": "2022-11-07T19:42:55.732600",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.714566",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "date         object\n",
       "article      object\n",
       "quantity    float64\n",
       "price        object\n",
       "dtype: object"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.dtypes"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "3d098cbe",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.751381Z",
     "iopub.status.busy": "2022-11-07T19:42:55.751063Z",
     "iopub.status.idle": "2022-11-07T19:42:55.756577Z",
     "shell.execute_reply": "2022-11-07T19:42:55.755711Z"
    },
    "papermill": {
     "duration": 0.016974,
     "end_time": "2022-11-07T19:42:55.758325",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.741351",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(234005, 4)"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "deb7adf1",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.777155Z",
     "iopub.status.busy": "2022-11-07T19:42:55.776878Z",
     "iopub.status.idle": "2022-11-07T19:42:55.780426Z",
     "shell.execute_reply": "2022-11-07T19:42:55.779604Z"
    },
    "papermill": {
     "duration": 0.014911,
     "end_time": "2022-11-07T19:42:55.782044",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.767133",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "# Fixing the price column from dtype == object to dtype == float"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "3b6e3345",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.800607Z",
     "iopub.status.busy": "2022-11-07T19:42:55.800364Z",
     "iopub.status.idle": "2022-11-07T19:42:55.804341Z",
     "shell.execute_reply": "2022-11-07T19:42:55.803548Z"
    },
    "papermill": {
     "duration": 0.015159,
     "end_time": "2022-11-07T19:42:55.805974",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.790815",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "import numpy as np"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "08052868",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.824421Z",
     "iopub.status.busy": "2022-11-07T19:42:55.824181Z",
     "iopub.status.idle": "2022-11-07T19:42:55.828917Z",
     "shell.execute_reply": "2022-11-07T19:42:55.828137Z"
    },
    "papermill": {
     "duration": 0.016037,
     "end_time": "2022-11-07T19:42:55.830617",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.814580",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "def return_price_as_float(price):\n",
    "    # Price is currently as string, return it as float\n",
    "    try:\n",
    "        return np.float(price[0] + '.' + price[2] + price[3])\n",
    "    except:\n",
    "        return np.float(price[0])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "45b4f4d7",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:55.849356Z",
     "iopub.status.busy": "2022-11-07T19:42:55.849071Z",
     "iopub.status.idle": "2022-11-07T19:42:56.352477Z",
     "shell.execute_reply": "2022-11-07T19:42:56.351536Z"
    },
    "papermill": {
     "duration": 0.515167,
     "end_time": "2022-11-07T19:42:56.354728",
     "exception": false,
     "start_time": "2022-11-07T19:42:55.839561",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "/opt/conda/lib/python3.7/site-packages/ipykernel_launcher.py:4: DeprecationWarning: `np.float` is a deprecated alias for the builtin `float`. To silence this warning, use `float` by itself. Doing this will not modify any behavior and is safe. If you specifically wanted the numpy scalar type, use `np.float64` here.\n",
      "Deprecated in NumPy 1.20; for more details and guidance: https://numpy.org/devdocs/release/1.20.0-notes.html#deprecations\n",
      "  after removing the cwd from sys.path.\n",
      "/opt/conda/lib/python3.7/site-packages/ipykernel_launcher.py:6: DeprecationWarning: `np.float` is a deprecated alias for the builtin `float`. To silence this warning, use `float` by itself. Doing this will not modify any behavior and is safe. If you specifically wanted the numpy scalar type, use `np.float64` here.\n",
      "Deprecated in NumPy 1.20; for more details and guidance: https://numpy.org/devdocs/release/1.20.0-notes.html#deprecations\n",
      "  \n"
     ]
    }
   ],
   "source": [
    "df['price'] = df['price'].apply(lambda price: return_price_as_float(price))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "8b408d9f",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.373945Z",
     "iopub.status.busy": "2022-11-07T19:42:56.373686Z",
     "iopub.status.idle": "2022-11-07T19:42:56.399012Z",
     "shell.execute_reply": "2022-11-07T19:42:56.398413Z"
    },
    "papermill": {
     "duration": 0.037059,
     "end_time": "2022-11-07T19:42:56.400930",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.363871",
     "status": "completed"
    },
    "tags": []
   },
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
       "      <th>quantity</th>\n",
       "      <th>price</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>234005.000000</td>\n",
       "      <td>234005.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>1.538377</td>\n",
       "      <td>1.579405</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>1.289603</td>\n",
       "      <td>1.396841</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>-200.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.100000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>1.200000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.500000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>200.000000</td>\n",
       "      <td>9.800000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "            quantity          price\n",
       "count  234005.000000  234005.000000\n",
       "mean        1.538377       1.579405\n",
       "std         1.289603       1.396841\n",
       "min      -200.000000       0.000000\n",
       "25%         1.000000       1.100000\n",
       "50%         1.000000       1.200000\n",
       "75%         2.000000       1.500000\n",
       "max       200.000000       9.800000"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "f710410d",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.420882Z",
     "iopub.status.busy": "2022-11-07T19:42:56.420633Z",
     "iopub.status.idle": "2022-11-07T19:42:56.430288Z",
     "shell.execute_reply": "2022-11-07T19:42:56.429307Z"
    },
    "papermill": {
     "duration": 0.021885,
     "end_time": "2022-11-07T19:42:56.432223",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.410338",
     "status": "completed"
    },
    "tags": []
   },
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
       "      <th>date</th>\n",
       "      <th>article</th>\n",
       "      <th>quantity</th>\n",
       "      <th>price</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>BAGUETTE</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.90</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>PAIN AU CHOCOLAT</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1.20</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>PAIN AU CHOCOLAT</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.20</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>PAIN</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.15</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>TRADITIONAL BAGUETTE</td>\n",
       "      <td>5.0</td>\n",
       "      <td>1.20</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         date               article  quantity  price\n",
       "0  2021-01-02              BAGUETTE       1.0   0.90\n",
       "1  2021-01-02      PAIN AU CHOCOLAT       3.0   1.20\n",
       "2  2021-01-02      PAIN AU CHOCOLAT       2.0   1.20\n",
       "3  2021-01-02                  PAIN       1.0   1.15\n",
       "4  2021-01-02  TRADITIONAL BAGUETTE       5.0   1.20"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "23d5085a",
   "metadata": {
    "papermill": {
     "duration": 0.009641,
     "end_time": "2022-11-07T19:42:56.451343",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.441702",
     "status": "completed"
    },
    "tags": []
   },
   "source": [
    "#### Now to apply some encoding to the different items in the article column"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "16748561",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.472249Z",
     "iopub.status.busy": "2022-11-07T19:42:56.471496Z",
     "iopub.status.idle": "2022-11-07T19:42:56.695326Z",
     "shell.execute_reply": "2022-11-07T19:42:56.694440Z"
    },
    "papermill": {
     "duration": 0.236732,
     "end_time": "2022-11-07T19:42:56.697651",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.460919",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "dishes = pd.get_dummies(df['article'])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "88f70031",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.717924Z",
     "iopub.status.busy": "2022-11-07T19:42:56.717651Z",
     "iopub.status.idle": "2022-11-07T19:42:56.723389Z",
     "shell.execute_reply": "2022-11-07T19:42:56.722495Z"
    },
    "papermill": {
     "duration": 0.017875,
     "end_time": "2022-11-07T19:42:56.725190",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.707315",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "234005"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(dishes)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "38f33674",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.745415Z",
     "iopub.status.busy": "2022-11-07T19:42:56.745175Z",
     "iopub.status.idle": "2022-11-07T19:42:56.749248Z",
     "shell.execute_reply": "2022-11-07T19:42:56.748418Z"
    },
    "papermill": {
     "duration": 0.016505,
     "end_time": "2022-11-07T19:42:56.751261",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.734756",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "unique_dishes = list(dishes.columns)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "805254b2",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.771922Z",
     "iopub.status.busy": "2022-11-07T19:42:56.771422Z",
     "iopub.status.idle": "2022-11-07T19:42:56.849823Z",
     "shell.execute_reply": "2022-11-07T19:42:56.848997Z"
    },
    "papermill": {
     "duration": 0.0911,
     "end_time": "2022-11-07T19:42:56.852035",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.760935",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "from tqdm.auto import tqdm"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "22ddd221",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.872330Z",
     "iopub.status.busy": "2022-11-07T19:42:56.872041Z",
     "iopub.status.idle": "2022-11-07T19:42:56.903692Z",
     "shell.execute_reply": "2022-11-07T19:42:56.903149Z"
    },
    "papermill": {
     "duration": 0.043266,
     "end_time": "2022-11-07T19:42:56.905222",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.861956",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "application/vnd.jupyter.widget-view+json": {
       "model_id": "0a8119e678e042b1929664fd8283b985",
       "version_major": 2,
       "version_minor": 0
      },
      "text/plain": [
       "0it [00:00, ?it/s]"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "encoding = {}\n",
    "\n",
    "for index, dishes in tqdm(enumerate(unique_dishes)):\n",
    "    encoding[dishes] = index"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "80d8868d",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:56.926939Z",
     "iopub.status.busy": "2022-11-07T19:42:56.925977Z",
     "iopub.status.idle": "2022-11-07T19:42:57.576548Z",
     "shell.execute_reply": "2022-11-07T19:42:57.575275Z"
    },
    "papermill": {
     "duration": 0.663545,
     "end_time": "2022-11-07T19:42:57.578742",
     "exception": false,
     "start_time": "2022-11-07T19:42:56.915197",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "import seaborn as sns\n",
    "import matplotlib.pyplot as plt"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "73f3b586",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:57.599983Z",
     "iopub.status.busy": "2022-11-07T19:42:57.598981Z",
     "iopub.status.idle": "2022-11-07T19:42:57.603693Z",
     "shell.execute_reply": "2022-11-07T19:42:57.603018Z"
    },
    "papermill": {
     "duration": 0.016803,
     "end_time": "2022-11-07T19:42:57.605420",
     "exception": false,
     "start_time": "2022-11-07T19:42:57.588617",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "def return_encoding(item):\n",
    "    return encoding[item]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "id": "902c04d4",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:57.627317Z",
     "iopub.status.busy": "2022-11-07T19:42:57.626375Z",
     "iopub.status.idle": "2022-11-07T19:42:57.732351Z",
     "shell.execute_reply": "2022-11-07T19:42:57.731419Z"
    },
    "papermill": {
     "duration": 0.118619,
     "end_time": "2022-11-07T19:42:57.734632",
     "exception": false,
     "start_time": "2022-11-07T19:42:57.616013",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "df['article'] = df['article'].apply(lambda item: return_encoding(item))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "6d31a471",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:57.756375Z",
     "iopub.status.busy": "2022-11-07T19:42:57.756021Z",
     "iopub.status.idle": "2022-11-07T19:42:57.789492Z",
     "shell.execute_reply": "2022-11-07T19:42:57.788638Z"
    },
    "papermill": {
     "duration": 0.047196,
     "end_time": "2022-11-07T19:42:57.791716",
     "exception": false,
     "start_time": "2022-11-07T19:42:57.744520",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "df['date'] = pd.DatetimeIndex(df['date'])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "b400bbc8",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:57.813935Z",
     "iopub.status.busy": "2022-11-07T19:42:57.813631Z",
     "iopub.status.idle": "2022-11-07T19:42:57.823716Z",
     "shell.execute_reply": "2022-11-07T19:42:57.823152Z"
    },
    "papermill": {
     "duration": 0.022468,
     "end_time": "2022-11-07T19:42:57.825244",
     "exception": false,
     "start_time": "2022-11-07T19:42:57.802776",
     "status": "completed"
    },
    "tags": []
   },
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
       "      <th>date</th>\n",
       "      <th>article</th>\n",
       "      <th>quantity</th>\n",
       "      <th>price</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>4</td>\n",
       "      <td>1.0</td>\n",
       "      <td>0.90</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>85</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1.20</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>85</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.20</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>84</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1.15</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>140</td>\n",
       "      <td>5.0</td>\n",
       "      <td>1.20</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "        date  article  quantity  price\n",
       "0 2021-01-02        4       1.0   0.90\n",
       "1 2021-01-02       85       3.0   1.20\n",
       "2 2021-01-02       85       2.0   1.20\n",
       "3 2021-01-02       84       1.0   1.15\n",
       "4 2021-01-02      140       5.0   1.20"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2486fbfa",
   "metadata": {
    "papermill": {
     "duration": 0.009461,
     "end_time": "2022-11-07T19:42:57.844718",
     "exception": false,
     "start_time": "2022-11-07T19:42:57.835257",
     "status": "completed"
    },
    "tags": []
   },
   "source": [
    "#### Simple Task: Lets just look at simplified forecasting for now, just the date and the revenue"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "61e3fda2",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:57.865773Z",
     "iopub.status.busy": "2022-11-07T19:42:57.865057Z",
     "iopub.status.idle": "2022-11-07T19:42:58.693011Z",
     "shell.execute_reply": "2022-11-07T19:42:58.692167Z"
    },
    "papermill": {
     "duration": 0.840851,
     "end_time": "2022-11-07T19:42:58.695190",
     "exception": false,
     "start_time": "2022-11-07T19:42:57.854339",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "dates = list(pd.get_dummies(df['date']).columns)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "id": "4212c797",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:58.716372Z",
     "iopub.status.busy": "2022-11-07T19:42:58.715967Z",
     "iopub.status.idle": "2022-11-07T19:42:58.722776Z",
     "shell.execute_reply": "2022-11-07T19:42:58.721379Z"
    },
    "papermill": {
     "duration": 0.019626,
     "end_time": "2022-11-07T19:42:58.724873",
     "exception": false,
     "start_time": "2022-11-07T19:42:58.705247",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "600"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(dates)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "id": "2ba6f912",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:58.746626Z",
     "iopub.status.busy": "2022-11-07T19:42:58.746135Z",
     "iopub.status.idle": "2022-11-07T19:42:58.753877Z",
     "shell.execute_reply": "2022-11-07T19:42:58.753264Z"
    },
    "papermill": {
     "duration": 0.020261,
     "end_time": "2022-11-07T19:42:58.755459",
     "exception": false,
     "start_time": "2022-11-07T19:42:58.735198",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0      0.90\n",
       "1      1.20\n",
       "2      1.20\n",
       "3      1.15\n",
       "4      1.20\n",
       "       ... \n",
       "360    1.80\n",
       "361    1.50\n",
       "362    0.15\n",
       "363    0.15\n",
       "364    1.50\n",
       "Name: price, Length: 365, dtype: float64"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Looping Framework\n",
    "df['price'].loc[df['date'] == dates[0]]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "id": "f7f17ebb",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:58.777041Z",
     "iopub.status.busy": "2022-11-07T19:42:58.776730Z",
     "iopub.status.idle": "2022-11-07T19:42:58.785006Z",
     "shell.execute_reply": "2022-11-07T19:42:58.784460Z"
    },
    "papermill": {
     "duration": 0.021261,
     "end_time": "2022-11-07T19:42:58.786781",
     "exception": false,
     "start_time": "2022-11-07T19:42:58.765520",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0      0.90\n",
       "1      3.60\n",
       "2      2.40\n",
       "3      1.15\n",
       "4      6.00\n",
       "       ... \n",
       "360    1.80\n",
       "361    1.50\n",
       "362    0.15\n",
       "363    0.15\n",
       "364    1.50\n",
       "Length: 365, dtype: float64"
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['quantity'].loc[df['date'] == '2021-01-02'] * df['price'].loc[df['date'] == '2021-01-02']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "id": "0c50d90f",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:58.809544Z",
     "iopub.status.busy": "2022-11-07T19:42:58.808960Z",
     "iopub.status.idle": "2022-11-07T19:42:58.815911Z",
     "shell.execute_reply": "2022-11-07T19:42:58.814959Z"
    },
    "papermill": {
     "duration": 0.020136,
     "end_time": "2022-11-07T19:42:58.817526",
     "exception": false,
     "start_time": "2022-11-07T19:42:58.797390",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "866.8499999999987"
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "sum(df['quantity'].loc[df['date'] == '2021-01-02'] * df['price'].loc[df['date'] == '2021-01-02'])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "id": "523280c2",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:58.838305Z",
     "iopub.status.busy": "2022-11-07T19:42:58.838038Z",
     "iopub.status.idle": "2022-11-07T19:42:59.730173Z",
     "shell.execute_reply": "2022-11-07T19:42:59.729172Z"
    },
    "papermill": {
     "duration": 0.904482,
     "end_time": "2022-11-07T19:42:59.731964",
     "exception": false,
     "start_time": "2022-11-07T19:42:58.827482",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "application/vnd.jupyter.widget-view+json": {
       "model_id": "e19bb988e9b048b780dbf1e879c90dd8",
       "version_major": 2,
       "version_minor": 0
      },
      "text/plain": [
       "  0%|          | 0/600 [00:00<?, ?it/s]"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "revenues = []\n",
    "\n",
    "for date in tqdm(dates):\n",
    "    # Each date has n number of rows which contain prices, and quantities. Multiplying them gets the net earning\n",
    "    revenue = sum(df['quantity'].loc[df['date'] == date] * df['price'].loc[df['date'] == date])\n",
    "    revenues.append(revenue)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "id": "2c921af8",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:59.755903Z",
     "iopub.status.busy": "2022-11-07T19:42:59.755555Z",
     "iopub.status.idle": "2022-11-07T19:42:59.761462Z",
     "shell.execute_reply": "2022-11-07T19:42:59.760655Z"
    },
    "papermill": {
     "duration": 0.020048,
     "end_time": "2022-11-07T19:42:59.763232",
     "exception": false,
     "start_time": "2022-11-07T19:42:59.743184",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(600, 600)"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(revenues), len(dates)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "6fcd525d",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:59.786722Z",
     "iopub.status.busy": "2022-11-07T19:42:59.786364Z",
     "iopub.status.idle": "2022-11-07T19:42:59.794098Z",
     "shell.execute_reply": "2022-11-07T19:42:59.793509Z"
    },
    "papermill": {
     "duration": 0.021401,
     "end_time": "2022-11-07T19:42:59.795645",
     "exception": false,
     "start_time": "2022-11-07T19:42:59.774244",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "data = pd.DataFrame()\n",
    "data['ds'] = dates\n",
    "data['y'] = revenues"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "id": "da8f96aa",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:59.817879Z",
     "iopub.status.busy": "2022-11-07T19:42:59.817510Z",
     "iopub.status.idle": "2022-11-07T19:42:59.826967Z",
     "shell.execute_reply": "2022-11-07T19:42:59.826147Z"
    },
    "papermill": {
     "duration": 0.022525,
     "end_time": "2022-11-07T19:42:59.828831",
     "exception": false,
     "start_time": "2022-11-07T19:42:59.806306",
     "status": "completed"
    },
    "tags": []
   },
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
       "      <th>ds</th>\n",
       "      <th>y</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2021-01-02</td>\n",
       "      <td>866.85</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2021-01-03</td>\n",
       "      <td>838.30</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2021-01-04</td>\n",
       "      <td>461.90</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2021-01-05</td>\n",
       "      <td>493.70</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2021-01-07</td>\n",
       "      <td>478.00</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          ds       y\n",
       "0 2021-01-02  866.85\n",
       "1 2021-01-03  838.30\n",
       "2 2021-01-04  461.90\n",
       "3 2021-01-05  493.70\n",
       "4 2021-01-07  478.00"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "8736384f",
   "metadata": {
    "papermill": {
     "duration": 0.010669,
     "end_time": "2022-11-07T19:42:59.850633",
     "exception": false,
     "start_time": "2022-11-07T19:42:59.839964",
     "status": "completed"
    },
    "tags": []
   },
   "source": [
    "### Forecasting Revenues"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "id": "d8e4ce50",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:42:59.873401Z",
     "iopub.status.busy": "2022-11-07T19:42:59.873135Z",
     "iopub.status.idle": "2022-11-07T19:43:00.078043Z",
     "shell.execute_reply": "2022-11-07T19:43:00.076661Z"
    },
    "papermill": {
     "duration": 0.219648,
     "end_time": "2022-11-07T19:43:00.081266",
     "exception": false,
     "start_time": "2022-11-07T19:42:59.861618",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [],
   "source": [
    "from prophet import Prophet"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "id": "2476d492",
   "metadata": {
    "execution": {
     "iopub.execute_input": "2022-11-07T19:43:00.111239Z",
     "iopub.status.busy": "2022-11-07T19:43:00.110838Z",
     "iopub.status.idle": "2022-11-07T19:43:01.882584Z",
     "shell.execute_reply": "2022-11-07T19:43:01.881590Z"
    },
    "papermill": {
     "duration": 1.790483,
     "end_time": "2022-11-07T19:43:01.885239",
     "exception": false,
     "start_time": "2022-11-07T19:43:00.094756",
     "status": "completed"
    },
    "tags": []
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "19:43:00 - cmdstanpy - INFO - Chain [1] start processing\n",
      "19:43:00 - cmdstanpy - INFO - Chain [1] done processing\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "Text(0.5, 1.0, 'Prophet Model forecasts on Bakery Sales')"
      ]
     },
     "execution_count": 37,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsgAAAG4CAYAAABYYREqAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMywgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/NK7nSAAAACXBIWXMAAAsTAAALEwEAmpwYAAEAAElEQVR4nOydd5xWxb3/P+dpS1k6CCwiohADKNIWeARxFRQ1ig1LjEavLTExXk03xpsY8xNTTCzRGLyWmEQxMSqJ3YuujYemYMMCBhRY6vbdp5wy8/tjzpw6s4DuyiLf931ds8xzzsycec4z853vfIvBOecgCIIgCIIgCAIAkNjTHSAIgiAIgiCIzgQJyARBEARBEAQRgARkgiAIgiAIgghAAjJBEARBEARBBCABmSAIgiAIgiACkIBMEARBEARBEAFIQCYI4nPj/vvvx/Tp0/d0N3YbwzCwdu3anV5XXV2N/fffX/v5a6+9hpEjR6K8vByPP/54O/aQ0PHzn/8c55133p7uxm6xN/aZIL5okIBMEAQOPPBAdO3aFeXl5Rg4cCAuvPBCtLS07OluhdgV4bqqqgqGYeDNN98MlZ922mkwDAPV1dUd2MOd8z//8z+44oor0NLSglNPPXWP9mVX2NWNQUdSXV2NRCKB8vJylJeXY8iQIfjZz362R/u0KzQ0NOCiiy7CoEGD0KNHD3zpS1/CTTfdtKe7RRDELkICMkEQAIB///vfaGlpwRtvvIEVK1bgl7/8Zewa27b3QM92jy996Ut44IEHvH/X1tYil8thwIABe7BXgo8//hhjxoz5VPfuDWPfUVRUVKClpQUtLS149dVXcc8993zuGvjdHf+rr74aLS0teO+999DY2Ih//etfGDFiRAf1jiCI9oYEZIIgQgwZMgQnnHAC3nnnHQBCi3jHHXdg5MiRGDlyJADg7rvvxogRI9C3b1/MmTMHNTU13v2GYeC2227DQQcdhP79++MHP/gBGGOhNr7//e+jT58+GD58OJ5++mmvvLGxERdffDEGDx6MIUOG4Kc//Skcx8F7772Hb37zm8jlcigvL0fv3r21/f/a176Ghx9+GI7jAAAeeughnHbaachkMt41pVIJV111FSoqKlBRUYGrrroKpVLJ+/w3v/kNBg8ejIqKCtx7772h+kulEr7//e/jgAMOwMCBA/HNb34ThUJhp+N68MEH4z//+Q9OPvlklJeXo1QqoaamBnPmzEHfvn0xYsQI3H333d71P//5zzF37lycd9556NmzJ+6//37t+EjuvvtujBo1Cj169MDo0aPxxhtvAABuuukmHHzwwV75Y4895t2zdu1aHHXUUejVqxf69++Ps88+GwAwY8YMAMDhhx+O8vJyPPzww9ixYwdOOukk9O7dG3379sWRRx4Z+24lixcvRmVlJXr16oXKykosXrzY+6yqqgrXXXcdpk2bhh49euC4447Djh07djqGADB8+HAcccQRWL16tVf23//93xg6dCh69uyJiRMn4pVXXlHea1kWvvrVr+KMM86AaZqoqanBGWecgQEDBmD48OG47bbbtON/0003oVu3bqitrfWueeONNzBgwABYlhVra/ny5Tj33HPRp08fJBIJfPnLX8bcuXN3u88AsGTJEhxxxBHo3bs3Dj/88NBJyP3334+DDjoIPXr0wPDhw/G3v/1tl8aRIIidwAmC2OcZNmwYf/755znnnH/yySd89OjR/Kc//SnnnHMAfNasWby2tpbn83m+aNEi3q9fP/7666/zYrHIr7jiCn7kkUd6dQHgVVVVvLa2ln/88cd85MiR/O677+acc37ffffxVCrF58+fz23b5nfeeScfPHgwZ4xxzjk/9dRT+WWXXcZbWlr41q1beWVlJb/rrru8e6dNm9bmcxx11FH87rvv5sceeyx/6qmnOOecV1ZW8sWLF/MhQ4bwF198kXPO+XXXXcenTJnCt27dyrdt28az2az3vE8//TTfb7/9+Ntvv81bWlr4V7/6VQ6Ar1mzhnPO+VVXXcVPPvlkXltby5uamvhJJ53Ef/zjH3POOX/xxRf5kCFDdmmcOef8yCOP5JdffjkvFAp85cqVvH///nzRokWcc85/9rOf8VQqxR977DHuOA7P5/Ntjs/f//53XlFRwZctW8YZY3zNmjV8/fr13mebNm3ijuPwBQsW8G7duvGamhrOOefnnHMO/+Uvf8kdx+GFQoG/8soroe9SPjfnnP/4xz/m3/jGN7hpmtw0Tf7yyy97312Q2tpa3rt3b/7AAw9wy7L4gw8+yHv37s137NjhfU8HHXQQ/+CDD3g+n+dHHXUU/9GPfqQcs+iYfvjhh7yiosIbJ845/8tf/sJ37NjBLcviv/3tb/nAgQN5oVDwxvFrX/saz+fz/MQTT+QXXHABt22bO47DJ0yYwK+//npeKpX4Rx99xIcPH86feeYZ7fifcMIJ/M477/Taveqqq/gVV1yh7PfFF1/MR48eze+9917+4Ycfxj7flT5zzvnGjRt53759+ZNPPskdx+HPPfcc79u3L9+2bRtvaWnhPXr04O+//z7nnPOamhr+zjvvKPtDEMTuQQIyQRB82LBhvHv37rxXr178gAMO4JdffjnP5/OccyEkBYWRiy66iP/gBz/w/t3c3MxTqRRft26dd/3TTz/tfX7HHXfwY445hnMuhNyDDz7Y+6y1tZUD4Js3b+ZbtmzhmUzGa5dzzh988EFeVVXl3burAvJf/vIXfs455/D33nuPjxw5knPOQwLyQQcdxJ988knvvmeeeYYPGzaMc875f/3Xf4WEtQ8++MATFBljvFu3bnzt2rXe54sXL+YHHngg53z3BORPPvmEJxIJ3tTU5H3+4x//mF9wwQWccyEkBTceOxuf4447jt9yyy1tjo/k8MMP548//jjnnPPzzz+fX3rppXzDhg2x66IC8nXXXcfnzJkTKlPxwAMP8MrKylDZ1KlT+X333cc5F9/TDTfc4H12xx138NmzZyvrevHFF7lhGLxXr168R48eHAA/7bTTeKlU0rbfu3dvvmrVKs65GMeTTz6Zz5gxg3/nO9/xBPolS5bwoUOHhu678cYb+YUXXujdFxx/zjlfsGABP+KIIzjnnNu2zQcOHMiXLl2q7EM+n+f/7//9Pz5hwgSeSqX4wQcf7G3adqXPUkC+6aab+HnnnRe69rjjjuP3338/b2lp4b169eKPPPJI6L0gCOKzQyYWBEEAAB5//HE0NDTg448/xp133omuXbt6nw0dOtT7u6amBsOGDfP+XV5ejn79+mHTpk3K64cNGxYywRg0aJD3d7du3QAALS0t+Pjjj2FZFgYPHozevXujd+/e+MY3voFt27bt9rOcfvrpeOGFF/CHP/wB559/fuzz6DME+1hTUxPrv2T79u3I5/OYOHGi18fjjz8e27dv3+0+1tTUoG/fvujRo0eoLd047mx8NmzYgIMPPljZ1gMPPIBx48Z5973zzjueScOvf/1rcM4xefJkjBkzJmZSEuQHP/gBRowYgeOOOw4HHXSQ1uksOr6qZ4u+B205hVZUVKChoQFNTU1oaGhA165dccEFF3if//a3v8WoUaPQq1cv9O7dG42NjSGTjSVLluCtt97Cj3/8YxiGAUCMZ01NjTcmvXv3xo033oitW7d69wXHHwBOOeUUrF69GuvWrcPzzz+PXr16YfLkyco+d+3aFT/5yU/w+uuvo7a2FmeddRbOPPNM1NXV7VKfJR9//DH+8Y9/hPr56quvYvPmzejevTsefvhh3HXXXRg8eDC+8pWv4P3339eOI0EQu05qT3eAIIjOjxQqACGsfPzxx96/W1tbUVtbiyFDhnhlGzZs8JzRPvnkE1RUVOy0jaFDh6KsrAw7duxAKhWfmoJ92BndunXDCSecgD/+8Y/46KOPYp/LZ1D1cfDgwdiwYYN37SeffOL93b9/f3Tt2hXvvvtu6Hk/DRUVFairq0Nzc7MnJH/yySeheoPPvLPxGTp0qPJZP/74Y1x66aVYtGgRstkskskkxo0bB845ACGoStvnV199FbNmzcKMGTOUDmU9evTAzTffjJtvvhnvvPMOjjnmGFRWVmLmzJmxZwu+I/LZjj/++F0dHi29evXCueee69lKv/LKK/j1r3+NRYsWYcyYMUgkEujTp4/3fABw3HHHYezYsZg5cyaqq6sxcOBADB06FMOHD8eaNWu0bUXfuS5duuCss87CX//6V7z//vvKzZeKnj174ic/+QnmzZuHdevW4d13391pnyVDhw7F+eefH7JPDzJ79mzMnj0bhUIBP/3pT3HppZe2ac9MEMSuQRpkgiB2i69+9au47777sGrVKpRKJfzkJz/BlClTcOCBB3rX/OY3v0F9fT02bNiAW2+91RNm2mLw4ME47rjj8L3vfQ9NTU1gjOGjjz7CSy+9BAAYOHAgNm7cCNM0d6mfN954I1566aVQv4LP8Mtf/hLbt2/Hjh078Itf/MKLO3vWWWfh/vvvx+rVq5HP53H99dd79yUSCVx66aW4+uqrPc3tpk2b8Oyzz+5Sn4IMHToURxxxBK655hoUi0W89dZbuOeee7Txb3c2Ppdccgl++9vf4vXXXwfnHGvXrsXHH3+M1tZWGIbhRfG47777PAdMAPjHP/6BjRs3AgD69OkDwzCQSIilYeDAgfjPf/7jXfvEE09g7dq14JyjV69eSCaT3rVBTjzxRHz44Yd48MEHYds2Hn74YaxevRonnXTSbo9TlJaWFixYsMDb3DQ3NyOVSmHAgAGwbRu/+MUv0NTUFLvvhz/8Ic4991zMnDkTO3bswOTJk9GjRw/86le/QqFQgOM4eOedd7B8+fI22//617+O+++/H//617/aFJBvuOEGLF++HKZpolgs4tZbb0Xv3r1xyCGH7HKfAeC8887Dv//9bzz77LNwHAfFYhHV1dXYuHEjtm7dioULF6K1tRVlZWUoLy9Xfh8EQew+9EsiCGK3mDVrFm644QacccYZGDx4MD766CMsWLAgdM0pp5yCiRMnYty4cfjKV76Ciy++eJfqfuCBB2CaJkaPHo0+ffpg7ty52Lx5MwDgmGOOwZgxYzBo0CD0799/p3VVVFRo4yb/9Kc/xaRJkzB27FgcdthhmDBhAn76058CAE444QRcddVVOOaYYzBixAgcc8wxoXt/9atfYcSIEZg6dSp69uyJWbNm4YMPPtil54vy0EMPYf369aioqMBpp52G66+/HrNmzdJe39b4nHnmmbj22mtx7rnnokePHjj11FNRV1eH0aNH43vf+x6y2SwGDhyIt99+G9OmTfPqXL58OaZMmYLy8nLMmTMHt956Kw466CAAIpLDBRdcgN69e+Pvf/871qxZg1mzZqG8vBzZbBbf+ta3cPTRR8f62a9fPzzxxBO4+eab0a9fP/z617/GE088sUvfm4qamhovDvKwYcNQV1fnRWuYPXs2jj/+eHzpS1/CsGHD0KVLl5hphOS6667DqaeeilmzZqGxsRFPPPEEVq1aheHDh6N///645JJL0NjY2GZfpk2bhkQigQkTJsTMSIIYhoH/+q//Qv/+/VFRUYHnn38eTz75JMrLy3erz0OHDsXChQtx4403YsCAARg6dCh+85vfgDEGxhh+97vfoaKiAn379sVLL72EP/7xj7s4qgRBtIXBVWc6BEEQnxLDMLBmzRqK+Up8YTnmmGNw7rnn4pJLLtnTXSEIooMgG2SCIAiC2EWWL1+ON954AwsXLtzTXSEIogMhEwuCIAiC2AUuuOACzJo1C7fcckso+ghBEF88yMSCIAiCIAiCIAKQBpkgCIIgCIIgAnwhbZD79++vDO30RcKyLKTT6T3djb0SGrv2gcaxfaBxbB9oHD89NHbtA41j+/B5j+P69euVSXq+kALygQceiBUrVuzpbnQoNTU1u5R8gYhDY9c+0Di2DzSO7QON46eHxq59oHFsHz7vcZw0aZKynEwsCIIgCIIgCCIACcgEQRAEQRAEEYAE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\n",
      "text/plain": [
       "<Figure size 720x432 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "pre = Prophet()\n",
    "pre.fit(data)\n",
    "future = pre.make_future_dataframe(periods=30)\n",
    "\n",
    "#Create a dataset to forcast market prices. \n",
    "forecast = pre.predict(future)\n",
    "# data_forecast = forecast[[\"Date\",\"Close\",\"yhat_upper\"]]\n",
    "# pd.set_option('display.max_rows',data_forecast.shape[0]+1)\n",
    "\n",
    "# Ploting out Binance BTC market predictions.\n",
    "pre.plot(forecast)\n",
    "plt.legend(['Actual','Predicted'])\n",
    "plt.title(\"Prophet Model forecasts on Bakery Sales\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "76b0ecf6",
   "metadata": {
    "papermill": {
     "duration": 0.012168,
     "end_time": "2022-11-07T19:43:01.910223",
     "exception": false,
     "start_time": "2022-11-07T19:43:01.898055",
     "status": "completed"
    },
    "tags": []
   },
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
   "version": "3.7.12"
  },
  "papermill": {
   "default_parameters": {},
   "duration": 14.069594,
   "end_time": "2022-11-07T19:43:02.642639",
   "environment_variables": {},
   "exception": null,
   "input_path": "__notebook__.ipynb",
   "output_path": "__notebook__.ipynb",
   "parameters": {},
   "start_time": "2022-11-07T19:42:48.573045",
   "version": "2.3.4"
  },
  "widgets": {
   "application/vnd.jupyter.widget-state+json": {
    "state": {
     "03a08e415e294da1b44b8972cec56b7e": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": null
      }
     },
     "098d1b1fd0664a4ba3c80414c4b3b293": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "ProgressStyleModel",
      "state": {
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "ProgressStyleModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "StyleView",
       "bar_color": null,
       "description_width": ""
      }
     },
     "0a8119e678e042b1929664fd8283b985": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "HBoxModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "HBoxModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "HBoxView",
       "box_style": "",
       "children": [
        "IPY_MODEL_da151c357560463faaf1ff8619027784",
        "IPY_MODEL_ca0faf9de5304c13b21791a30d75266b",
        "IPY_MODEL_1955578da19b433c9b5c9d2e974dd0d6"
       ],
       "layout": "IPY_MODEL_fdacb36c6b79431d98d071059bd4f73f"
      }
     },
     "1955578da19b433c9b5c9d2e974dd0d6": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "HTMLModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "HTMLModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "HTMLView",
       "description": "",
       "description_tooltip": null,
       "layout": "IPY_MODEL_530d52579d70464d9afca109e31d3a92",
       "placeholder": "​",
       "style": "IPY_MODEL_ea85eb91c1644bc797290efc84eb7ad2",
       "value": " 149/? [00:00&lt;00:00, 6420.49it/s]"
      }
     },
     "332fd721d4d34972bbca6978310f5745": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": null
      }
     },
     "376c4d1572f344508d0e30a706a2e714": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "DescriptionStyleModel",
      "state": {
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "DescriptionStyleModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "StyleView",
       "description_width": ""
      }
     },
     "48e19a1ff2c647f8baa18f01887cd3e9": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": null
      }
     },
     "530d52579d70464d9afca109e31d3a92": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": null
      }
     },
     "58a92bbd7c3d4013815f6070c6d0b4ab": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "ProgressStyleModel",
      "state": {
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "ProgressStyleModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "StyleView",
       "bar_color": null,
       "description_width": ""
      }
     },
     "a05ac2edf0aa4f1fb03cbf083a5634f9": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": null
      }
     },
     "a17135b52dd64fb1a0850ffbcc693e2f": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "DescriptionStyleModel",
      "state": {
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "DescriptionStyleModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "StyleView",
       "description_width": ""
      }
     },
     "a88ac1ed345d4d0592ff11c5dc191b68": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "HTMLModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "HTMLModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "HTMLView",
       "description": "",
       "description_tooltip": null,
       "layout": "IPY_MODEL_a05ac2edf0aa4f1fb03cbf083a5634f9",
       "placeholder": "​",
       "style": "IPY_MODEL_376c4d1572f344508d0e30a706a2e714",
       "value": " 600/600 [00:00&lt;00:00, 690.96it/s]"
      }
     },
     "ad76d2935c9548d2a33817e10128a86d": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "HTMLModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "HTMLModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "HTMLView",
       "description": "",
       "description_tooltip": null,
       "layout": "IPY_MODEL_48e19a1ff2c647f8baa18f01887cd3e9",
       "placeholder": "​",
       "style": "IPY_MODEL_a17135b52dd64fb1a0850ffbcc693e2f",
       "value": "100%"
      }
     },
     "ca0faf9de5304c13b21791a30d75266b": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "FloatProgressModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "FloatProgressModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "ProgressView",
       "bar_style": "success",
       "description": "",
       "description_tooltip": null,
       "layout": "IPY_MODEL_ea0e4597f7274c31ade4bbe47495476d",
       "max": 1.0,
       "min": 0.0,
       "orientation": "horizontal",
       "style": "IPY_MODEL_58a92bbd7c3d4013815f6070c6d0b4ab",
       "value": 1.0
      }
     },
     "da151c357560463faaf1ff8619027784": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "HTMLModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "HTMLModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "HTMLView",
       "description": "",
       "description_tooltip": null,
       "layout": "IPY_MODEL_03a08e415e294da1b44b8972cec56b7e",
       "placeholder": "​",
       "style": "IPY_MODEL_f828500ed1bb4d91bb9bb685970b6e9d",
       "value": ""
      }
     },
     "e19bb988e9b048b780dbf1e879c90dd8": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "HBoxModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "HBoxModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "HBoxView",
       "box_style": "",
       "children": [
        "IPY_MODEL_ad76d2935c9548d2a33817e10128a86d",
        "IPY_MODEL_e546dde58a3c4674a5127d2b2d361d8c",
        "IPY_MODEL_a88ac1ed345d4d0592ff11c5dc191b68"
       ],
       "layout": "IPY_MODEL_e1f193e9743442b4b03303de0b6cc365"
      }
     },
     "e1f193e9743442b4b03303de0b6cc365": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": null
      }
     },
     "e546dde58a3c4674a5127d2b2d361d8c": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "FloatProgressModel",
      "state": {
       "_dom_classes": [],
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "FloatProgressModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/controls",
       "_view_module_version": "1.5.0",
       "_view_name": "ProgressView",
       "bar_style": "success",
       "description": "",
       "description_tooltip": null,
       "layout": "IPY_MODEL_332fd721d4d34972bbca6978310f5745",
       "max": 600.0,
       "min": 0.0,
       "orientation": "horizontal",
       "style": "IPY_MODEL_098d1b1fd0664a4ba3c80414c4b3b293",
       "value": 600.0
      }
     },
     "ea0e4597f7274c31ade4bbe47495476d": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": "20px"
      }
     },
     "ea85eb91c1644bc797290efc84eb7ad2": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "DescriptionStyleModel",
      "state": {
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "DescriptionStyleModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "StyleView",
       "description_width": ""
      }
     },
     "f828500ed1bb4d91bb9bb685970b6e9d": {
      "model_module": "@jupyter-widgets/controls",
      "model_module_version": "1.5.0",
      "model_name": "DescriptionStyleModel",
      "state": {
       "_model_module": "@jupyter-widgets/controls",
       "_model_module_version": "1.5.0",
       "_model_name": "DescriptionStyleModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "StyleView",
       "description_width": ""
      }
     },
     "fdacb36c6b79431d98d071059bd4f73f": {
      "model_module": "@jupyter-widgets/base",
      "model_module_version": "1.2.0",
      "model_name": "LayoutModel",
      "state": {
       "_model_module": "@jupyter-widgets/base",
       "_model_module_version": "1.2.0",
       "_model_name": "LayoutModel",
       "_view_count": null,
       "_view_module": "@jupyter-widgets/base",
       "_view_module_version": "1.2.0",
       "_view_name": "LayoutView",
       "align_content": null,
       "align_items": null,
       "align_self": null,
       "border": null,
       "bottom": null,
       "display": null,
       "flex": null,
       "flex_flow": null,
       "grid_area": null,
       "grid_auto_columns": null,
       "grid_auto_flow": null,
       "grid_auto_rows": null,
       "grid_column": null,
       "grid_gap": null,
       "grid_row": null,
       "grid_template_areas": null,
       "grid_template_columns": null,
       "grid_template_rows": null,
       "height": null,
       "justify_content": null,
       "justify_items": null,
       "left": null,
       "margin": null,
       "max_height": null,
       "max_width": null,
       "min_height": null,
       "min_width": null,
       "object_fit": null,
       "object_position": null,
       "order": null,
       "overflow": null,
       "overflow_x": null,
       "overflow_y": null,
       "padding": null,
       "right": null,
       "top": null,
       "visibility": null,
       "width": null
      }
     }
    },
    "version_major": 2,
    "version_minor": 0
   }
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
