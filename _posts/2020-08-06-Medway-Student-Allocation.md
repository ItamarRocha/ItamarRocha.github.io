---
layout: post
title: Medway Student Allocation
date: 2020-08-08
---

### What is medway?

<center>
<div>
 <img src="https://raw.githubusercontent.com/ItamarRocha/ItamarRocha.github.io/master/images/medway/medway.jpg" alt="logo_medway" style="width:550px">
</div>
</center>

[Medway João Pessoa](https://www.instagram.com/medwayjp/) is a preparatory course for ENEM (Brazilian SAT) and other tests (private universities). Medway has more than 200 students enrolled and counts with a system that's different from its competitors. The difference relies on the way the company treats its students. Medway has several workers that have experience with ENEM and are responsible for advising the students in their studies and life. These employees are called *assessor* (some kind of Advisor/Organizer) who usually are students that have already passed the ENEM with high scores and are considered communicative.
<hr>

### Problem Overview

The problem here is that each advisor has normally 16 students with whom he must speak weekly, to know how they are doing on their studies, how were their grades on the mock tests, and how are they doing in general. However, these students are allocated without constraints. Therefore, some advisors get students that are not 100% compatible with them, and that need more attention during the week. These two problems are responsible for difficulting the job and for burning out some of the advisors.

With this scenario in mind, my main objective in this work was trying to make things more balanced, so the students and the advisors can enjoy their roles in the best way possible while having a maximized total compatibility.
<hr>

### Tools Used

During the project I have decided to use:
* [CPLEX optimizer](https://www.ibm.com/analytics/cplex-optimizer) (C++) from IBM as the mixed integer programming (MIP) solver.
* Python libraries such as Pandas and Numpy for the preprocessing phase.
* Google Forms to collect the data
<hr>

### Data Production

In view of this, I thought of crafting some sort of compatibility metric. With the help of my bosses and some of the college professors, I have made a Google forms with questions about different aspects of each student and each advisor's life. Some of the information that was asked is listed below:

* Age
* Gender
* Degree that he/she intends to pursuit
* Organization Level
* Religion
* Extrovertion level
* Sensibility level
* Prefered subject
* Political views
* and many others...

The main concern in asking so many questions from different life aspects was to make a good compatibility modeling.

After deciding the questions, I have sent the Google Forms link for all the 250+ students and all the 18 advisors. After that I made another document where I asked each advisor to write how much time they used to spend with each of their students in the following scale (In minutes):
<center>
  <div>
    <table border = "1">
        <tr>
            <td>between 5</td>
            <td>between 5 and 10</td>
            <td>between 10 and 15</td>
            <td>between 15 and 20</td>
            <td>between 20 and 25</td>
            <td>25+</td>
        </tr>
        <tr>
            <td>0</td>
            <td>1</td>
            <td>2</td>
            <td>3</td>
            <td>4</td>
            <td>5</td>
        </tr>
    </table>
  </div>
</center>

As in all project that depends on too many factors, although all the advisors had responded, I ended up with 170 student responses.
<hr>

### Preprocessing

To compute the compatibility matrix, as the main objective of this project is to model the problem matematically and allocate the students, I chose a simple correlation function. The matrix consists of a $i \ x \ j$ matrix, where i is the number of students and j is the number of advisors.

For each question with equal responses it was computed +1 in the pair [student,advisor].

Some of the questions were also used for constraints purposes. The preference for the advisor being from the same sex, for example, resulted in a negative M in the compatibility matrix, therefore eliminating that possibility. I also determined that each advisor could only receive students that were in a maximum one year older than them, adding new big negatives Ms in the matrix.

The result was the following table:

<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: center;
    }

    .dataframe tbody tr th {
        vertical-align: center;
    }

    .dataframe thead th {
        text-align: center;
    }
</style>
<table class="dataframe" border="1">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A0</th>
      <th>A1</th>
      <th>A2</th>
      <th>A3</th>
      <th>A4</th>
      <th>A5</th>
      <th>A6</th>
      <th>A7</th>
      <th>A8</th>
      <th>A9</th>
      <th>A10</th>
      <th>...</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>S0</th>
      <td>11</td>
      <td>-10000</td>
      <td>-10000</td>
      <td>15</td>
      <td>-10000</td>
      <td>13</td>
      <td>-10000</td>
      <td>13</td>
      <td>-10000</td>
      <td>16</td>
      <td>-10000</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S1</th>
      <td>12</td>
      <td>13</td>
      <td>10</td>
      <td>13</td>
      <td>14</td>
      <td>10</td>
      <td>12</td>
      <td>13</td>
      <td>16</td>
      <td>15</td>
      <td>14</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S2</th>
      <td>14</td>
      <td>-10000</td>
      <td>-10000</td>
      <td>18</td>
      <td>-10000</td>
      <td>13</td>
      <td>-10000</td>
      <td>16</td>
      <td>-10000</td>
      <td>20</td>
      <td>-10000</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S3</th>
      <td>-10000</td>
      <td>14</td>
      <td>-10000</td>
      <td>-10000</td>
      <td>-10000</td>
      <td>14</td>
      <td>12</td>
      <td>-10000</td>
      <td>17</td>
      <td>-10000</td>
      <td>-10000</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S4</th>
      <td>12</td>
      <td>16</td>
      <td>11</td>
      <td>16</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>15</td>
      <td>15</td>
      <td>13</td>
      <td>10</td>
      <td>...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S152</th>
      <td>12</td>
      <td>11</td>
      <td>9</td>
      <td>11</td>
      <td>13</td>
      <td>14</td>
      <td>13</td>
      <td>14</td>
      <td>11</td>
      <td>13</td>
      <td>11</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S153</th>
      <td>11</td>
      <td>10</td>
      <td>13</td>
      <td>10</td>
      <td>11</td>
      <td>13</td>
      <td>12</td>
      <td>10</td>
      <td>11</td>
      <td>12</td>
      <td>11</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S154</th>
      <td>14</td>
      <td>16</td>
      <td>13</td>
      <td>11</td>
      <td>13</td>
      <td>15</td>
      <td>9</td>
      <td>17</td>
      <td>17</td>
      <td>13</td>
      <td>15</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S155</th>
      <td>10</td>
      <td>-10000</td>
      <td>-10000</td>
      <td>12</td>
      <td>-10000</td>
      <td>11</td>
      <td>-10000</td>
      <td>13</td>
      <td>-10000</td>
      <td>13</td>
      <td>-10000</td>
      <td>...</td>
    </tr>
    <tr>
      <th>S156</th>
      <td>14</td>
      <td>11</td>
      <td>12</td>
      <td>10</td>
      <td>10</td>
      <td>12</td>
      <td>8</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>12</td>
      <td>...</td>
    </tr>
  </tbody>
</table>
<p>157 rows × 15 columns</p>
</div>

> The names and the preprocessing scripts were omitted since the information gathered in this project is private and was not authorized to be published.

 <hr>

### Modeling
#### Sets
* $S \ \rightarrow$ Students
* $A \ \rightarrow$ Advisors

#### Data
* $c_{i,j} \ \rightarrow$ Compatibility of student(i) and advisor(j)
* $w_{i} \ \rightarrow$ Weight of time spent by student i.
* $f_{j} \ \rightarrow$ Fixed Students
* $t_{j} \ \rightarrow$ Fixed Weight of Time of advisor j.

The fixed time and fixed students were done in order to overcome the limitations proportioned by the lack of responses by some students. I chose to maintain the students that didn't respond to the survey as fixed with their advisors. With that said, the advisor already starts this allocation process with $f_{j}$ students and $t_{j}$ time.

#### Constants
* $N \ \rightarrow$ The average number of students per advisor. 
* $T \ \rightarrow$ The average time that each advisor spents with all its students during the week.

#### Decision variables
The decision variable here is 

$x_{i,j} \ \in \ \{0,1\}$

where x is a boolean 2D array that tells if a student(i) is allocated with an advisor(j) or not.

#### Objective Function  
Our goal is to maximize the total compatibility. With that said, our objective function is:  
  
$$
\sum_{i \in S} \sum_{j \in A} c_{i,j} x_{i,j}
$$

#### Constraints

1. **Each student must have only one advisor**  
  
$$
\sum_{j \in A} x_{i,j} = 1 \ , \ \forall i \ \in S
$$

2. **Limiting the number of students per advisor**  
  
$$
f_{j} + \sum_{i \in S} x_{i,j} = N \ , \forall j \ \in A
$$
  
* The ideal case would be that all the advisors have the same number of students. However, is not always possible since the division may not result in an integer. The solution is to set a small interval {N-1,N+1}.

3. **Limiting the time spent by each advisor**  
  
$$
t_j + \sum_{i \in S} w_i x_{i,j} = T \ , \forall j \ \in A
$$
  
* Just like the previous constraint, we may also have to change this constraint to two different ones, bounding it to an interval.
<hr>
### Results and Comparisons
Using the model that I have made led to an optimal solution to the problem. Apart from having the maximum compatibility possible (using the metric previously presented), the problem also tackled 
the imbalances in the previous allocation.

The average time is 60 (in the scale of time mentioned in data production). However, before using the model, the standard deviation of each advisor's time was 11.65, which was reduced to 0.8. In addition, the number of students for each advisor's standard deviation was 1.18 and ended up being 0.5.

In summary, the modeling was able to distribute the students to maximizing the compatibility and balancing the job for each advisor, since they all get paid the same.

> The optimization code can be found [here](https://github.com/ItamarRocha/Operations-Research/tree/master/projects/medway)
<hr>

### Improvements and Future Works

Improvements:
* Gather the data from all students.
* Test other compatibility metrics.

Future works:

* Develop a software to do the allocation automatically.
* Create a prediction of the time spent by the new students based on interview informations.
<hr>

### Questions?

You can reach me out on any social media at the end of the page.