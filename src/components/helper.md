{data: 
        [
            {
            val1:
            val2:
            generationmix   [
                                {
                                fuel:
                                perc:
                                }
                                {
                                fuel:
                                perc:   
                                }...                           
                            ]
            },
            {   

            },
            {
            }...
}
divider = data.lenght*48

data.forEach(object){
    object.generationmix.forEach(genmixObject){
        resultingList
    }
    
}


const fruits = [
  {
    apples: 4,
    pears: 6,
    oranges: 2,
  },
  {
    bananas: 2,
    oranges: 5,
  },
  {
    pears: 8,
    apples: 3,
    bananas: 10,
  },
  {},
  {
    pears: 7,
    apples: 5,
  },
  {
    mangos: 1,
  },
];

const mergeFruits = data => {
  const result = {}; 

  data.forEach(basket => { 
    for (let [key, value] of Object.entries(basket)) { 
      if (result[key]) { 
        result[key] += value; 
      } else { 
        result[key] = value;
      }
    }
  });
  return result; 
};


const basket = fruits.reduce((basket, fruit) => {
    for (const [fruitName, fruitCount] of Object.entries(fruit)) {
        if (!basket[fruitName]) {
            basket[fruitName] = 0;
        }

        basket[fruitName] += fruitCount;
    }

    return basket;
}, {});

<!-- tim's version of above -->
data.data will be list, [ { generationmix: [ {fuel:<fuel>}, (perc:<perc>) ], ...  }, ... ]
objectList will be { generationmix: [ {fuel:<fuel>}, (perc:<perc>) ], ...  }




      averager(list){
        let newListOfObjects = []
        for(let i = 0; i<list.length; i++){
            for(let j = 0; j<list[i].generationmix.length; j++){
                if (!newListOfObjects[j]) {
                    newListOfObjects[j] = {'fuel':list[i].generationmix[j].fuel, 'perc':list[i].generationmix[j].perc}
                } else {
                    newListOfObjects[j].perc += list[i].generationmix[j].perc
                }
            }
        }
        newListOfObjects.forEach((object)=>{
            object.perc =/ list.length
        })
        console.log(newListOfObjects)
      }