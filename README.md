### BD Lab Internal Assessment
```
Submitted by:-
Sagar M
1NT18IS130
```

#### Part 1:- MongoDB

- Demonstrate the usage of $match, $group, aggregate pipelines.
```sh
> db.data.aggregate([
... { $match: { "Years of Service": 5 } },
... { $group: { _id: "$Years of Service", average: { $avg: "$Salary" } } }
... ])
{ "_id" : 5, "average" : 135413.33333333334 }
```


- Demonstrate the Map-Reduce aggregate function on this dataset.
```sh
> var mapFunction1 = function() {
	emit(this.Years_of_Service, this.Salary);
};
> var reduceFunction1 = function(numYearServed, Salaries) {
	return Array.sum(Salaries);
};
> db.data.mapReduce(
	mapFunction1,
	reduceFunction1,
	{ out: "map_reduce_output" }
)
{ "result" : "map_reduce_output", "ok" : 1 }
> db.map_reduce_output.find().pretty()
```

- Find out all the Employees, who are paying tax>50000 and are not eligible for pay raise.
```sh
db.data.find( 
	{ $and: [ { Tax: { $gt: 50000 } } ,
		{ Eligible_for_Pay_Raise: false } ] 
} ).pretty()
```

- Demonstrate the Alter and Drop commands on this dataset.
```sh
> db.data.update( { Years_of_Service: 6 }, { $inc: { No_of_Increments: 1 } } )
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
>

> db.data.drop()
true
>
```

#### Part 2:- Hadoop

- [Find out the total number of employees who are eligible for pay raise](hadoop/Program1.java)
- [Find out the cumulative years of service done by the employees for the company](hadoop/Program2.java)

