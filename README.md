# "Surf's Up" Analysis Using Python and SQLAlchemy

## Overview of Analysis

### Purpose
The purpose of this analysis was to show the temperature data for the months of June and December in Oahu in order to determine if a surf and ice cream shop business is sustainable year-round.

## Results
I first imported the dependencies for NumPy, Pandas, and SQLAlchemy as I was querying a SQLite database.

```
import numpy as np
import pandas as pd

import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine, func
```

I then created an engine, set up a base class for an automap schema, and created a session link to the database.

```
engine = create_engine("sqlite:///hawaii.sqlite")

Base = automap_base()
Base.prepare(engine, reflect=True)

Measurement = Base.classes.measurement
Station = Base.classes.station

session = Session(engine)
```

To find the temperature data for the month of June in Oahu, I wrote a query that filters the date column from the Measurement table and converted the June temperatures to a list.

``
from sqlalchemy import extract

june_results = []
june_query = session.query(Measurement.date, Measurement.tobs).filter(extract('month', Measurement.date) == 6)

june_results = list(june_query)
```

