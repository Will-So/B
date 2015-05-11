
Todo
====

1. Add df.describe() functionality
2. Transpose
3. CSV Slicing
4. Where
5. Print the values like in Pandas
6. Exponents
7. Pivot tables
8. Odo R `data <https://github.com/ContinuumIO/odo/issues/121>`__
9. Join docstring is not useful

.. code:: python

    import sys
    sys.path.append('/Users/Will/Devel/git/blaze/')
    sys.path.reverse()
    import blaze
    print(blaze.__file__)


.. parsed-literal::

    /Users/Will/Devel/git/blaze/blaze/__init__.pyc


.. code:: python

    import warnings
    warnings.filterwarnings("ignore")

10 Minutes to Blaze
===================

This section provides a short introduction for Blaze. After reading this
section, beginners should know how to do basic data operations with
blaze [rephrase].

.. code:: python

    import blaze as bz
    from blaze import odo

Data Input and Output
=====================

Data used in this section can be found
`here <https://github.com/Will-So/blaze_data>`__. The interface for
reading different data types is consistent. With all data stores, we use
the ``Data`` object to load the data.

Reading from a CSV
------------------

.. code:: python

    from blaze import Data

.. code:: python

    iris = Data(DATA_DIR + 'iris.csv')
    iris.head(3)




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>sepal_length</th>
          <th>sepal_width</th>
          <th>petal_length</th>
          <th>petal_width</th>
          <th>species</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>5.1</td>
          <td>3.5</td>
          <td>1.4</td>
          <td>0.2</td>
          <td>Iris-setosa</td>
        </tr>
        <tr>
          <th>1</th>
          <td>4.9</td>
          <td>3.0</td>
          <td>1.4</td>
          <td>0.2</td>
          <td>Iris-setosa</td>
        </tr>
        <tr>
          <th>2</th>
          <td>4.7</td>
          <td>3.2</td>
          <td>1.3</td>
          <td>0.2</td>
          <td>Iris-setosa</td>
        </tr>
      </tbody>
    </table>



Reading from an SQL Database
----------------------------

.. code:: python

    db = Data('sqlite:////' + DATA_DIR + 'lahman2013.sqlite')

We can use the ``fields`` attribute to look at a list of the tables in
the database. Note that with Ipython you can also type ``db.<TAB>`` to
see all the tables. Alternatively, simply print ``db.fields`` to view
all the tables.

.. code:: python

    print(db.fields,)


.. parsed-literal::

    ([u'AllstarFull', u'Appearances', u'AwardsManagers', u'AwardsPlayers', u'AwardsShareManagers', u'AwardsSharePlayers', u'Batting', u'BattingPost', u'Fielding', u'FieldingOF', u'FieldingPost', u'HallOfFame', u'Managers', u'ManagersHalf', u'Master', u'Pitching', u'PitchingPost', u'Salaries', u'Schools', u'SchoolsPlayers', u'SeriesPost', u'Teams', u'TeamsFranchises', u'TeamsHalf', u'temp'],)


.. code:: python

    df = db.Batting
    df.head(3)




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>playerID</th>
          <th>yearID</th>
          <th>stint</th>
          <th>teamID</th>
          <th>lgID</th>
          <th>G</th>
          <th>G_batting</th>
          <th>AB</th>
          <th>R</th>
          <th>H</th>
          <th>2B</th>
          <th>3B</th>
          <th>HR</th>
          <th>RBI</th>
          <th>SB</th>
          <th>CS</th>
          <th>BB</th>
          <th>SO</th>
          <th>IBB</th>
          <th>HBP</th>
          <th>SH</th>
          <th>SF</th>
          <th>GIDP</th>
          <th>G_old</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>aardsda01</td>
          <td>2004</td>
          <td>1</td>
          <td>SFN</td>
          <td>NL</td>
          <td>11</td>
          <td>11</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>11</td>
        </tr>
        <tr>
          <th>1</th>
          <td>aardsda01</td>
          <td>2006</td>
          <td>1</td>
          <td>CHN</td>
          <td>NL</td>
          <td>45</td>
          <td>43</td>
          <td>2</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>45</td>
        </tr>
        <tr>
          <th>2</th>
          <td>aardsda01</td>
          <td>2007</td>
          <td>1</td>
          <td>CHA</td>
          <td>AL</td>
          <td>25</td>
          <td>2</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>2</td>
        </tr>
      </tbody>
    </table>



Reading from HDF5
-----------------

First, we take a look at the ``File Object`` of the HDF5 files.

.. code:: python

    Data(DATA_DIR + 'sample.hdf5').fields




.. parsed-literal::

    ['info', 'points', 'z']



So now we see that there are three different datasets in the file. We
pick the one we are interested in:

.. code:: python

    hdfs_df = Data(DATA_DIR + 'sample.hdf5::/z')
    hdfs_df[:2]




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>z</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>0.628902</td>
        </tr>
        <tr>
          <th>1</th>
          <td>0.797281</td>
        </tr>
      </tbody>
    </table>



Dealing with HDF5 files is somewhat more complex than most types of
files. More details for dealing with HDF5 files can be found
`here <https://odo.readthedocs.org/en/latest/hdf5.html>`__.

Reading Other Files
-------------------

Most other supported backends can be loaded in the same way that we load
HDF5 and SQL. A notable exception is Spark. If you need to use Spark
with Blaze, the documentation
`here <http://odo.readthedocs.org/en/latest/spark.html>`__ provides an
excellent walkthrough.

As of version 0.8, supported backends include AWS, CSV, JSON, HDF5,
Hadoop File System, Hive, Mongo, Spark/SQL, SAS, SQL, and SSH.

Writing files
-------------

The Blaze ecosystem also makes it to save data into new formats.

.. code:: python

    odo(df, DATA_DIR + 'baseball.csv')




.. parsed-literal::

    <odo.backends.csv.CSV at 0x110d15f10>



Viewing Data
============

See the top and bottom rows of our dataset.

.. code:: python

    df.head(5)




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>playerID</th>
          <th>yearID</th>
          <th>stint</th>
          <th>teamID</th>
          <th>lgID</th>
          <th>G</th>
          <th>G_batting</th>
          <th>AB</th>
          <th>R</th>
          <th>H</th>
          <th>2B</th>
          <th>3B</th>
          <th>HR</th>
          <th>RBI</th>
          <th>SB</th>
          <th>CS</th>
          <th>BB</th>
          <th>SO</th>
          <th>IBB</th>
          <th>HBP</th>
          <th>SH</th>
          <th>SF</th>
          <th>GIDP</th>
          <th>G_old</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>aardsda01</td>
          <td>2004</td>
          <td>1</td>
          <td>SFN</td>
          <td>NL</td>
          <td>11</td>
          <td>11</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>11</td>
        </tr>
        <tr>
          <th>1</th>
          <td>aardsda01</td>
          <td>2006</td>
          <td>1</td>
          <td>CHN</td>
          <td>NL</td>
          <td>45</td>
          <td>43</td>
          <td>2</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>45</td>
        </tr>
        <tr>
          <th>2</th>
          <td>aardsda01</td>
          <td>2007</td>
          <td>1</td>
          <td>CHA</td>
          <td>AL</td>
          <td>25</td>
          <td>2</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>2</td>
        </tr>
        <tr>
          <th>3</th>
          <td>aardsda01</td>
          <td>2008</td>
          <td>1</td>
          <td>BOS</td>
          <td>AL</td>
          <td>47</td>
          <td>5</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>5</td>
        </tr>
        <tr>
          <th>4</th>
          <td>aardsda01</td>
          <td>2009</td>
          <td>1</td>
          <td>SEA</td>
          <td>AL</td>
          <td>73</td>
          <td>3</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>NaN</td>
        </tr>
      </tbody>
    </table>



Blaze also offers a number of ways to interactively look at our
datasets.

We can select a single column using either df[``column_name``\ ] or
df.\ ``column_name``. The former allows us to select multiple columns at
once.

.. code:: python

    df[['teamID', 'G', 'H']][:3]




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>teamID</th>
          <th>G</th>
          <th>H</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>SFN</td>
          <td>11</td>
          <td>0</td>
        </tr>
        <tr>
          <th>1</th>
          <td>CHN</td>
          <td>45</td>
          <td>0</td>
        </tr>
        <tr>
          <th>2</th>
          <td>CHA</td>
          <td>25</td>
          <td>0</td>
        </tr>
      </tbody>
    </table>



Selecting via ``[]`` can also be useful

.. code:: python

    df[1000:1002]




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>playerID</th>
          <th>yearID</th>
          <th>stint</th>
          <th>teamID</th>
          <th>lgID</th>
          <th>G</th>
          <th>G_batting</th>
          <th>AB</th>
          <th>R</th>
          <th>H</th>
          <th>2B</th>
          <th>3B</th>
          <th>HR</th>
          <th>RBI</th>
          <th>SB</th>
          <th>CS</th>
          <th>BB</th>
          <th>SO</th>
          <th>IBB</th>
          <th>HBP</th>
          <th>SH</th>
          <th>SF</th>
          <th>GIDP</th>
          <th>G_old</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>allench01</td>
          <td>2000</td>
          <td>1</td>
          <td>MIN</td>
          <td>AL</td>
          <td>15</td>
          <td>15</td>
          <td>50</td>
          <td>2</td>
          <td>15</td>
          <td>3</td>
          <td>0</td>
          <td>0</td>
          <td>7</td>
          <td>0</td>
          <td>2</td>
          <td>3</td>
          <td>14</td>
          <td>0</td>
          <td>1</td>
          <td>0</td>
          <td>1</td>
          <td>1</td>
          <td>15</td>
        </tr>
        <tr>
          <th>1</th>
          <td>allench01</td>
          <td>2001</td>
          <td>1</td>
          <td>MIN</td>
          <td>AL</td>
          <td>57</td>
          <td>57</td>
          <td>175</td>
          <td>20</td>
          <td>46</td>
          <td>13</td>
          <td>2</td>
          <td>4</td>
          <td>20</td>
          <td>1</td>
          <td>2</td>
          <td>19</td>
          <td>37</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>1</td>
          <td>7</td>
          <td>57</td>
        </tr>
      </tbody>
    </table>



For most backends other than SQL, we can also select data via location
using the following syntax: ``df[[1,3, 6]]``. This collects the 2nd,
4th, and 7th elements of the dataest.

.. code:: python

    hdfs_df[[1,3,6]]




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>z</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>0.797281</td>
        </tr>
        <tr>
          <th>1</th>
          <td>0.047750</td>
        </tr>
        <tr>
          <th>2</th>
          <td>0.772755</td>
        </tr>
      </tbody>
    </table>



Filtering Data
--------------

We can use ``isin`` for basic conditional logic. Here we select a row
only if years are in 2008 and 2010.

.. code:: python

    df[df.yearID.isin([2008, 2010])][:5]




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>playerID</th>
          <th>yearID</th>
          <th>stint</th>
          <th>teamID</th>
          <th>lgID</th>
          <th>G</th>
          <th>G_batting</th>
          <th>AB</th>
          <th>R</th>
          <th>H</th>
          <th>2B</th>
          <th>3B</th>
          <th>HR</th>
          <th>RBI</th>
          <th>SB</th>
          <th>CS</th>
          <th>BB</th>
          <th>SO</th>
          <th>IBB</th>
          <th>HBP</th>
          <th>SH</th>
          <th>SF</th>
          <th>GIDP</th>
          <th>G_old</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>aardsda01</td>
          <td>2008</td>
          <td>1</td>
          <td>BOS</td>
          <td>AL</td>
          <td>47</td>
          <td>5</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>5</td>
        </tr>
        <tr>
          <th>1</th>
          <td>aardsda01</td>
          <td>2010</td>
          <td>1</td>
          <td>SEA</td>
          <td>AL</td>
          <td>53</td>
          <td>4</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>NaN</td>
        </tr>
        <tr>
          <th>2</th>
          <td>abadfe01</td>
          <td>2010</td>
          <td>1</td>
          <td>HOU</td>
          <td>NL</td>
          <td>22</td>
          <td>22</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>1</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>0</td>
          <td>NaN</td>
        </tr>
        <tr>
          <th>3</th>
          <td>abercre01</td>
          <td>2008</td>
          <td>1</td>
          <td>HOU</td>
          <td>NL</td>
          <td>34</td>
          <td>34</td>
          <td>55</td>
          <td>10</td>
          <td>17</td>
          <td>5</td>
          <td>0</td>
          <td>2</td>
          <td>5</td>
          <td>5</td>
          <td>2</td>
          <td>1</td>
          <td>23</td>
          <td>0</td>
          <td>2</td>
          <td>1</td>
          <td>1</td>
          <td>0</td>
          <td>34</td>
        </tr>
        <tr>
          <th>4</th>
          <td>abreubo01</td>
          <td>2008</td>
          <td>1</td>
          <td>NYA</td>
          <td>AL</td>
          <td>156</td>
          <td>156</td>
          <td>609</td>
          <td>100</td>
          <td>180</td>
          <td>39</td>
          <td>4</td>
          <td>20</td>
          <td>100</td>
          <td>22</td>
          <td>11</td>
          <td>73</td>
          <td>109</td>
          <td>2</td>
          <td>1</td>
          <td>0</td>
          <td>1</td>
          <td>14</td>
          <td>156</td>
        </tr>
      </tbody>
    </table>



We can also select rows based on the values of a single columns. Here we
select the rows where players have gotten more than 255 hits a year.

.. code:: python

    df[df.H > 255]




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>playerID</th>
          <th>yearID</th>
          <th>stint</th>
          <th>teamID</th>
          <th>lgID</th>
          <th>G</th>
          <th>G_batting</th>
          <th>AB</th>
          <th>R</th>
          <th>H</th>
          <th>2B</th>
          <th>3B</th>
          <th>HR</th>
          <th>RBI</th>
          <th>SB</th>
          <th>CS</th>
          <th>BB</th>
          <th>SO</th>
          <th>IBB</th>
          <th>HBP</th>
          <th>SH</th>
          <th>SF</th>
          <th>GIDP</th>
          <th>G_old</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>sislege01</td>
          <td>1920</td>
          <td>1</td>
          <td>SLA</td>
          <td>AL</td>
          <td>154</td>
          <td>154</td>
          <td>631</td>
          <td>137</td>
          <td>257</td>
          <td>49</td>
          <td>18</td>
          <td>19</td>
          <td>122</td>
          <td>42</td>
          <td>17</td>
          <td>46</td>
          <td>19</td>
          <td>NaN</td>
          <td>2</td>
          <td>13</td>
          <td>NaN</td>
          <td>NaN</td>
          <td>154</td>
        </tr>
        <tr>
          <th>1</th>
          <td>suzukic01</td>
          <td>2004</td>
          <td>1</td>
          <td>SEA</td>
          <td>AL</td>
          <td>161</td>
          <td>161</td>
          <td>704</td>
          <td>101</td>
          <td>262</td>
          <td>24</td>
          <td>5</td>
          <td>8</td>
          <td>60</td>
          <td>36</td>
          <td>11</td>
          <td>49</td>
          <td>63</td>
          <td>19</td>
          <td>4</td>
          <td>2</td>
          <td>3</td>
          <td>6</td>
          <td>161</td>
        </tr>
      </tbody>
    </table>



Dealing with Missing Data
=========================

Pending ``isnull`` implementation.

Operations
==========

Descriptive statistics
----------------------

.. code:: python

    df.count()




.. raw:: html

    97889



.. code:: python

    df.HR.value_counts()


::


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-66-53df56217c8b> in <module>()
    ----> 1 df.HR.value_counts()
    

    /Users/Will/Devel/git/blaze/blaze/expr/expressions.py in __getattr__(self, key)
        166             pass
        167         try:
    --> 168             result = object.__getattribute__(self, key)
        169         except AttributeError:
        170             fields = dict(zip(map(valid_identifier, self.fields),


    AttributeError: 'Field' object has no attribute 'value_counts'


.. code:: python

    df.H.max(), df.AB.max(), df.HR.max()




.. parsed-literal::

    (262, 716, 73)



.. code:: python

    df.H.mean()




.. raw:: html

    40.366883116883116



We can also combine these operations with the filtering operations
previously discussed.

.. code:: python

    df[df.AB > 100].H.mean()




.. raw:: html

    92.42354023984191



Basic Arithmetic
----------------

Basic arithemtic (``+``, ``-``, ``*``, ``/``) is also possible.

.. code:: python

    df1 = df.H * 2
    df1[400:405]




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>H</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>150</td>
        </tr>
        <tr>
          <th>1</th>
          <td>92</td>
        </tr>
        <tr>
          <th>2</th>
          <td>34</td>
        </tr>
        <tr>
          <th>3</th>
          <td>6</td>
        </tr>
        <tr>
          <th>4</th>
          <td>122</td>
        </tr>
      </tbody>
    </table>



Basic Descriptive Stats
-----------------------

.. code:: python

    df.H.count()




.. raw:: html

    91476



.. code:: python

    df.H.max()




.. raw:: html

    262



.. code:: python

    df[df.AB > 100].H.mean()




.. raw:: html

    92.42354023984191



Applying Functions
==================

Plotting
--------

The quickest way to make basic plots with datasets that can fit in
memory is to convert your dataset to a Pandas Dataframe. See the Pandas
`Plotting <http://pandas.pydata.org/pandas-docs/stable/visualization.html>`__
documentaiton for details.

.. code:: python

    import pandas as pd
    from odo import odo
    pandas_df = odo(df, pd.DataFrame)

.. code:: python

    import matplotlib
    matplotlib.style.use('ggplot')
    %pylab inline


.. parsed-literal::

    Populating the interactive namespace from numpy and matplotlib


.. code:: python

    _ = pandas_df.plot(kind='scatter', x='AB', y='H', alpha=.2) 



.. image:: 10%20Minutes%20Blaze_files/10%20Minutes%20Blaze_64_0.png


Operations
==========


Merging
=======

.. code:: python

    from blaze import join
    all_stars = db.AllstarFull

.. code:: python

    all_stars.head(2)




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>playerID</th>
          <th>yearID</th>
          <th>gameNum</th>
          <th>gameID</th>
          <th>teamID</th>
          <th>lgID</th>
          <th>GP</th>
          <th>startingPos</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>aaronha01</td>
          <td>1955</td>
          <td>0</td>
          <td>NLS195507120</td>
          <td>ML1</td>
          <td>NL</td>
          <td>1</td>
          <td>NaN</td>
        </tr>
        <tr>
          <th>1</th>
          <td>aaronha01</td>
          <td>1956</td>
          <td>0</td>
          <td>ALS195607100</td>
          <td>ML1</td>
          <td>NL</td>
          <td>1</td>
          <td>NaN</td>
        </tr>
      </tbody>
    </table>



.. code:: python

    ?join

.. code:: python

    all_star_stats = join(df, all_stars, ['playerID','yearID'])
    all_star_stats.head(4)




.. raw:: html

    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>playerID</th>
          <th>yearID</th>
          <th>stint</th>
          <th>teamID_left</th>
          <th>lgID_left</th>
          <th>G</th>
          <th>G_batting</th>
          <th>AB</th>
          <th>R</th>
          <th>H</th>
          <th>2B</th>
          <th>3B</th>
          <th>HR</th>
          <th>RBI</th>
          <th>SB</th>
          <th>CS</th>
          <th>BB</th>
          <th>SO</th>
          <th>IBB</th>
          <th>HBP</th>
          <th>SH</th>
          <th>SF</th>
          <th>GIDP</th>
          <th>G_old</th>
          <th>gameNum</th>
          <th>gameID</th>
          <th>teamID_right</th>
          <th>lgID_right</th>
          <th>GP</th>
          <th>startingPos</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>aaronha01</td>
          <td>1955</td>
          <td>1</td>
          <td>ML1</td>
          <td>NL</td>
          <td>153</td>
          <td>153</td>
          <td>602</td>
          <td>105</td>
          <td>189</td>
          <td>37</td>
          <td>9</td>
          <td>27</td>
          <td>106</td>
          <td>3</td>
          <td>1</td>
          <td>49</td>
          <td>61</td>
          <td>5</td>
          <td>3</td>
          <td>7</td>
          <td>4</td>
          <td>20</td>
          <td>153</td>
          <td>0</td>
          <td>NLS195507120</td>
          <td>ML1</td>
          <td>NL</td>
          <td>1</td>
          <td>NaN</td>
        </tr>
        <tr>
          <th>1</th>
          <td>aaronha01</td>
          <td>1956</td>
          <td>1</td>
          <td>ML1</td>
          <td>NL</td>
          <td>153</td>
          <td>153</td>
          <td>609</td>
          <td>106</td>
          <td>200</td>
          <td>34</td>
          <td>14</td>
          <td>26</td>
          <td>92</td>
          <td>2</td>
          <td>4</td>
          <td>37</td>
          <td>54</td>
          <td>6</td>
          <td>2</td>
          <td>5</td>
          <td>7</td>
          <td>21</td>
          <td>153</td>
          <td>0</td>
          <td>ALS195607100</td>
          <td>ML1</td>
          <td>NL</td>
          <td>1</td>
          <td>NaN</td>
        </tr>
        <tr>
          <th>2</th>
          <td>aaronha01</td>
          <td>1957</td>
          <td>1</td>
          <td>ML1</td>
          <td>NL</td>
          <td>151</td>
          <td>151</td>
          <td>615</td>
          <td>118</td>
          <td>198</td>
          <td>27</td>
          <td>6</td>
          <td>44</td>
          <td>132</td>
          <td>1</td>
          <td>1</td>
          <td>57</td>
          <td>58</td>
          <td>15</td>
          <td>0</td>
          <td>0</td>
          <td>3</td>
          <td>13</td>
          <td>151</td>
          <td>0</td>
          <td>NLS195707090</td>
          <td>ML1</td>
          <td>NL</td>
          <td>1</td>
          <td>9</td>
        </tr>
        <tr>
          <th>3</th>
          <td>aaronha01</td>
          <td>1958</td>
          <td>1</td>
          <td>ML1</td>
          <td>NL</td>
          <td>153</td>
          <td>153</td>
          <td>601</td>
          <td>109</td>
          <td>196</td>
          <td>34</td>
          <td>4</td>
          <td>30</td>
          <td>95</td>
          <td>4</td>
          <td>1</td>
          <td>59</td>
          <td>49</td>
          <td>16</td>
          <td>1</td>
          <td>0</td>
          <td>3</td>
          <td>21</td>
          <td>153</td>
          <td>0</td>
          <td>ALS195807080</td>
          <td>ML1</td>
          <td>NL</td>
          <td>1</td>
          <td>9</td>
        </tr>
      </tbody>
    </table>



Grouping
========


Converting Data
===============


Gotchas
=======

-  Transferring SQL files to a new format can take a long time.

Tips
====

-  It is not currently possible to change a dataset when using a
   ``Data`` object. When changing data is necessary, use ``odo`` to
   transform the data into a database or array technology of your choice
   (Pandas DataFrame, HDFS). See the ``odo``
   `documentation <https://odo.readthedocs.org/en/latest/>`__ for more
   information.
-  Categories.

No Read
=======

.. code:: python

    DATA_DIR = '/Users/Will/Data/blaze_data/'

