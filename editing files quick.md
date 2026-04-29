# SED

sed 's/localhost/production/g' config.go

sed just tells us what it is going to change 

the -i flag changes in 

# sed combined with find and exec 

find . -name '*.py' -exec sed -i 's/testing/tested/g' {} ;

