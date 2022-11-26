# javascriptExcercises


const prompt = require("prompt-sync")({ sigint: true });
const students = [{
    age: 32,
    examScores: [],
    gender: 'male',
    name: 'edu'
  },
  {
    age: 29,
    examScores: [],
    gender: 'female',
    name: 'silvia'
  }]

const availableMaleNames = ['pepe', 'juan', 'victor', 'Leo', 'francisco', 'carlos'];
const availableFemaleNames = ['cecilia', 'ana', 'luisa', 'silvia', 'isabel', 'virginia'];
const availableGenders = ['male', 'female'];
//For case 5
function randomItem(arr){
    arr.splice((Math.random() * arr.length) | 0, 1)
};
//For case 7
function isMaleOrFemale(arr){
    let studentIsMale = 0
    let studentIsFemale = 0
    for(let x of arr){
        if(arr.gender === "female"){
            studentIsFemale ++
        } else{
            studentIsMale ++
        }
    };
    console.log(studentIsMale,studentIsFemale)
};
// For case 8
function isOneGender(arr){
    let checkOne= 0
    for(let x of arr){
        if(x.gender === "female"){
            checkOne ++
        }
    }
    
    if(arr.length === checkOne){
        console.log("All students are Female")
    }else if(checkOne === 0){
        console.log("All students are Male")
    } else{
        console.log("There are " + (arr.length - checkOne) + " male students in this course and " + checkOne + " female students in this course.")
    }
};
//For case 10
function randomValList(unaLista){
    let randomIndex = Math.floor(Math.random() * unaLista.length); 
    let randomElement = unaLista[randomIndex];
    return randomElement
}

function getRandomNumber(min, max) {
    return Math.floor(Math.random() * (max - min) ) + min;
  }

function getAName(maleList, femaleList, aGender){    
    if(aGender === "female"){
        return randomValList(femaleList)
    } else{
        return randomValList(maleList)
    }
}  

//For case 16 and 17
function sumList(arr){
    return arr.reduce((a, b) => a + b, 0)
}

function meanList(arr){
    return sumList(arr) / arr.length
}

// Mostrar alumnos en forma de tabla 
function show_menu(){
    const reqNames = [
        '1. Mostrar en formato de tabla todos los alumnos.',
        '2. Mostrar por consola la cantidad de alumnos que hay en clase.',
        '3. Mostrar por consola todos los nombres de los alumnos.',
        '4. Eliminar el último alumno de la clase.',
        '5. Eliminar un alumno aleatoriamente de la clase.',
        '6. Mostrar por consola todos los datos de los alumnos que son chicas.',
        '7. Mostrar por consola el número de chicos y chicas que hay en la clase.',
        '8. Mostrar true o false por consola si todos los alumnos de la clase son chicas.',
        '9. Mostrar por consola los nombres de los alumnos que tengan entre 20 y 25 años.',
        '10. Añadir un alumno nuevo con los siguientes datos',
        '11. Mostrar por consola el nombre de la persona más joven de la clase.',
        '12. Mostrar por consola la edad media de todos los alumnos de la clase.',
        '13. ostrar por consola la edad media de las chicas de la clase.',
        '14. Añadir nueva nota a los alumnos. Por cada alumno de la clase, tendremos que calcular una nota de forma aleatoria(número entre 0 y 10) y añadirla a su listado de notas.',
        '15. Ordenar el array de alumnos alfabéticamente según su nombre.',
        '16. Mostrar por consola el alumno de la clase con las mejores notas.',
        '17. Mostrar por consola la nota media más alta de la clase y el nombre del alumno al que pertenece.',
        '18. Añadir un punto extra a cada nota existente de todos los alumnos. Recordad que la nota máxima posible es 10. Si los alumnos aún no tienen registrada ninguna nota, les pondremos un 10.',
    ]
    do {
        for(const name of reqNames){
            console.log(name);
        }
        const input = parseInt(prompt('Select an option:'));

        switch(input){
            case 1:
                console.table(students);
                break;

            case 2:
                console.log(`There are ${students.length} students in class`)
                break;

            case 3:
                console.log('Student names: ')
                console.log(students.map((x)=>x.name))
                break;

            case 4:
                students.pop();
                console.log(students);
                break;

            case 5:
                randomItem(students);
                console.log(students);
                break; 

            case 6:
                const femaleStudents = students.filter((x)=>x.gender === "female");
                console.log(femaleStudents);
                break;

            case 7:
                isMaleOrFemale(students);
                break;

            case 8:
                isOneGender(students);
                break;

            case 9:
                let studentsFrom20To25 = students.filter((x)=>x.age >= 20 && x.age <=25);
                let getNameBack = studentsFrom20To25.map((x)=>x.name)
                console.log(getNameBack);
                break;

            case 10:
                                
                const randomGender = randomValList(availableGenders);
                newStudent = {
                    age: getRandomNumber(20, 50),
                    examScores: [],
                    gender: randomGender,
                    name: getAName(availableMaleNames, availableFemaleNames, randomGender),
                };
                students.push(newStudent)
                console.log(newStudent)
                break;
            
            case 11:
                let minAge = students.reduce((prev, cur) => (cur.age < prev.age ? cur : prev));      
                console.log(minAge)
                break;

            case 12:
                const mediaEdad = students.reduce((total, next) => total + next.age, 0) / students.length;
                console.log(mediaEdad);
                break;

            case 13:
                const womanFinder = students.filter(({gender}) => gender === "female")
                const mediaEdadMujer = womanFinder.reduce((total, next) => total + next.age, 0) / students.length
                console.log(mediaEdadMujer);
                break;

            case 14:
                for(let x of students){
                    x.examScores.push(getRandomNumber(0, 10))
                }
                break;
            
            case 15:
                console.log(students.sort((a, b) => a.name.localeCompare(b.name)))
                break;

            case 16:
                let maxScStud = students.reduce((prev, cur) => {
                    return sumList(cur.examScores) > sumList(prev.examScores) ? cur : prev
                });
                console.log(maxScStud)
                break;
            
            case 17:
                let tempStuds = students.map(x => {
                    return {
                        name: x.name,
                        meanScore: meanList(x.examScores)
                    }
                });
                let maxMeanStud = tempStuds.reduce((prev, cur) => {
                    return cur.meanScore > prev.meanScore ? cur : prev
                });
                console.log(maxMeanStud)
                break;
            
            case 18:
                for(stdnt of students){
                    stdnt.examScores = stdnt.examScores.map(x => x >= 9 ? 10 : x + 1)
                    if(stdnt.examScores.length === 0){
                        stdnt.examScores.push(10)
                    }
                }
                break;

            default:
                console.log('Incorrect option');
                return;
        }
    } while(true)
}

show_menu()
