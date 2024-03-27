

Titular de la cuenta: Consulado General del Perú en Bilbao
Nombre del banco: Banco Santander
Número de cuenta: ES0200490018402713845246
Concepto: el trámite a realizarse y el nombre completo de la persona que realiza el tramite.
Ejemplo de cómo rellenar el Concepto: “Nombre del trámite – Juan Pérez Sánchez”



* https://github.com/gin-gonic/gin - My goto framework for writing microservices
* https://github.com/golang/mock - Auto generate mocks from interfaces for unit testing
* https://github.com/stretchr/testify#suite-package - I primarily use the suite package for a clear separation of setup and teardown during tests and the Require() to fail fast the test at the point of error

https://github.com/rs/zerolog - Fell in love with its fluent interface and  structural logging library

https://pkg.go.dev/golang.org/x/sync/errgroup - Managing goroutines which can return error in the idomatic go way

Because I like hashicorp's multierror, I created https://github.com/andrewstuart/multierrgroup which basically provides the same API but returns all errors encountered, if any.

https://github.com/jackc/pgx - excellent library for Postgre. Especially if you need PSQL specific features

github.com/doug-martin/goqu - SQL query builder. Don't like ORMs in general, didn't like GORM. The API is a bit verbose but it does the job and supports tons of SQL features including database specific ones.

github.com/pkg/errors - don't like how wrapping is done in standard library. This is better. Been using this library forever and it's even compatible with recent standard library changes.

github.com/stretchr/testify - very useful for tests

go.uber.org/automaxprocs - must-have for kubernetes deployments

https://github.com/go-gorm/gorm - database "orm"

https://github.com/shopspring/decimal - super useful when dealing with currency
https://github.com/satori/go.uuid - great for generating uuid's
https://github.com/sirupsen/logrus - go-to logger when i need something more than just pushing to stdout