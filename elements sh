#!/bin/bash

PSQL="psql --username=freecodecamp --dbname=periodic_table -t --no-align -c"

#If you run ./element.sh, it should output only "Please provide an element as an argument." and finish running.

#If you run ./element.sh 1, ./element.sh H, or ./element.sh Hydrogen, it should output only "The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius."

#If you run ./element.sh script with another element as input, you should get the same output but with information associated with the given element.

#If the argument input to your "element.sh" script doesn't exist as an "atomic_number", "symbol", or "name" in the database, the only output should be "I could not find that element in the database."

#must run script with an argument
##argument can be periodic_number (INT), symbol (VARCHAR?) 1-2, name (VARCHAR),
####if argument = INT, then search for X where periodic_number=argument; else if argument = VARCHAR -- if argument <= 2 characters, then search for X where symbol=argument, else search for X where name=argument
##if script is run with no argument, output "I could not find that element in the database."

#retrieve atomic_number, name, symbol, type, atomic_mass, melting_point_celsius, boiling_point_celsius, 

##"The element with atomic number <atomic_number> is <name> (<symbol>). It's a <type>, with a mass of <atomic_mass> amu. <name> has a melting point of <melting_point_celsius> celsius and a boiling point of <boiling_point_celsius> celsius."

FULL_TABLE=$($PSQL "SELECT * FROM elements FULL JOIN properties USING(atomic_number) FULL JOIN types USING(type_id)")


if [[ $# == 1 ]] ##if there's an argument
then
##echo "There is an argument"
  ##if argument is an INT, atomic_number
  if [[ $1 =~ ^[0-9]*$ ]]
  then
    ATOMIC_NUMBER=$($PSQL "SELECT atomic_number FROM elements FULL JOIN properties USING(atomic_number) FULL JOIN types USING(type_id) where atomic_number=$1")
##    echo "This is a number"
        #if atomic_number doesn't exist
        if [[ -z $ATOMIC_NUMBER ]]
        then
          echo I could not find that element in the database.
        else ##if atomic number DOES exist
          ##retrieve info
          ELEMENT_INFO=$($PSQL "SELECT type_id, atomic_number, symbol, name, atomic_mass, melting_point_celsius, boiling_point_celsius, type FROM  elements FULL JOIN properties USING(atomic_number) FULL JOIN types USING(type_id) where atomic_number=$1 ORDER BY atomic_number")

          echo "$ELEMENT_INFO" | while IFS="|" read TYPE_ID ATOM_NUM SYMBOL NAME ATOMIC_MASS MELTING_POINT BOILING_POINT TYPE 
           do
             #echo "$TYPE_ID"
             echo "The element with atomic number $ATOM_NUM is $NAME ($SYMBOL). It's a $TYPE, with a mass of $ATOMIC_MASS amu. $NAME has a melting point of $MELTING_POINT celsius and a boiling point of $BOILING_POINT celsius."
           done
        fi

   elif [[ $1 =~ ^[a-zA-Z]{1,2}$ ]] ##if argument is <= 2 characters / symbol
   then
    ##echo "This is a symbol"
      ATOMIC_SYMBOL=$($PSQL "SELECT symbol FROM elements FULL JOIN properties USING(atomic_number) FULL JOIN types USING(type_id) where symbol='$1'")
      
          #if symbol doesn't exist
          if [[ -z $ATOMIC_SYMBOL ]]
          then
            echo I could not find that element in the database.
          else ##if atomic symbol DOES exist
            ##retrieve info
            ELEMENT_INFO=$($PSQL "SELECT type_id, atomic_number, symbol, name, atomic_mass, melting_point_celsius, boiling_point_celsius, type FROM  elements FULL JOIN properties USING(atomic_number) FULL JOIN types USING(type_id) where symbol='$1'")

            echo "$ELEMENT_INFO" | while IFS="|" read TYPE_ID ATOM_NUM SYMBOL NAME ATOMIC_MASS MELTING_POINT BOILING_POINT TYPE 
            do
            
              echo "The element with atomic number $ATOM_NUM is $NAME ($SYMBOL). It's a $TYPE, with a mass of $ATOMIC_MASS amu. $NAME has a melting point of $MELTING_POINT celsius and a boiling point of $BOILING_POINT celsius."
            done
          fi





 # elif ##search name
  #  then
  else
      #echo "This is a name"
      ATOMIC_NAME=$($PSQL "SELECT symbol FROM elements FULL JOIN properties USING(atomic_number) FULL JOIN types USING(type_id) where name='$1'")
      
          #if name doesn't exist
          if [[ -z $ATOMIC_NAME ]]
          then
            echo I could not find that element in the database.
          else ##if name DOES exist
            ##retrieve info
            ELEMENT_INFO=$($PSQL "SELECT type_id, atomic_number, symbol, name, atomic_mass, melting_point_celsius, boiling_point_celsius, type FROM  elements FULL JOIN properties USING(atomic_number) FULL JOIN types USING(type_id) where name='$1'")

            echo "$ELEMENT_INFO" | while IFS="|" read TYPE_ID ATOM_NUM SYMBOL NAME ATOMIC_MASS MELTING_POINT BOILING_POINT TYPE 
            do
            
              echo "The element with atomic number $ATOM_NUM is $NAME ($SYMBOL). It's a $TYPE, with a mass of $ATOMIC_MASS amu. $NAME has a melting point of $MELTING_POINT celsius and a boiling point of $BOILING_POINT celsius."
            done
          fi





 

  fi




else ##if there's no argument
  echo Please provide an element as an argument.
fi
