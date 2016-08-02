* **Instructions:**

- Spend the next few ~15 minutes with your partner answering the following questions. You should be using the Sequelize Documentation (and whatever other references you find online).

	- Answer: What is Sequelize?
		-orm

	- Answer: What advantages does it offer?
		-easy to test
		-gives you support for syncing databases
		-
		-validation, resctricts to specific form of data
		complex SQL queries in simple syntax,

	- Answer: How do I install it? How do I incorporate it into my app?
		-npm install --save sequalize

	- Answer: What the heck is a Sequelize model? What role will it play?
		-a representation of table data for sequelize

	- Answer: Let's say I have the below table in MySQL. 

		| Country     | PhoneCode | Capital   | IndependenceYear |
		|-------------|-----------|-----------|------------------|
		| Afghanistan | 93        | Kabul     | 1919             |
		| Belarus     | 375       | Misk      | 1991             |
		| Netherlands | 31        | Amsterdam | 1648             |
		| Oman        | 968       | Muscat    | 1970             |
		| Zambia      | 260       | Lusaka    | 1964             |

		- How would I model it in Sequelize? 

			var tableName = sequelize.define('tableName', {
				Country: {
					type: Sequelize.STRING
				},
				PhoneCode: {
					type: Sequelize.INTEGER
				},
				Capital: {
					type: Sequelize.STRING
				},
				IndependenceYear: {
					type: Sequelize.INTEGER
				},
			},
			{
				freezeTableName: true // Model tableName will be the same as the model name
			});

			tableName.sync({force:true}).then(function () {
				//Table created
				return tableName.created({
					Country: 'Afghanistan',
					PhoneCode: 'Hancock',
					Capital: 'Kabul',
					IndependenceYear: '1919'
				});
			});


		- How would I query for all the records where the Independence Year was less than 50 years ago?

			tableName.findALL({
				where: {
					IndependenceYear: { $lite:50 }
				}
			});

		- How would I query the table, order it by descending Independence Years, and limit the results to just show 2 of the records. Skipping the first two? (i.e. Results: Zambia, Afghanistan)

			something.findall({
				limit: 2,
				offset: 2,
				[sequelize.fn('max', sequelize.col('IndependenceYear')), 'DESC']
			})

	- Bonus: What is umzug? How could I use umzug to create a table? 

			-Umzug is a framework agnostic migration tool for Node.js. Provides a clean API for running and rolling back tasks.