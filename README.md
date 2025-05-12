# progetto-informatica
kotlin 

CopiaModifica 

CucinaApp/ 
├── App.js 
├── components/ 
│   └── RecipeItem.js 
├── screens/ 
│   ├── HomeScreen.js 
│   └── RecipeDetailScreen.js 
└── data/ 
    └── recipes.js 
 

 



jsx 

CopiaModifica 

import React from 'react'; 
import { NavigationContainer } from '@react-navigation/native'; 
import { createStackNavigator } from '@react-navigation/stack'; 
import HomeScreen from './screens/HomeScreen'; 
import RecipeDetailScreen from './screens/RecipeDetailScreen'; 
 
const Stack = createStackNavigator(); 
 
export default function App() { 
  return ( 
    <NavigationContainer> 
      <Stack.Navigator initialRouteName="Home"> 
        <Stack.Screen name="Home" component={HomeScreen} /> 
        <Stack.Screen name="RecipeDetail" component={RecipeDetailScreen} options={{ title: 'Dettagli Ricetta' }} /> 
      </Stack.Navigator> 
    </NavigationContainer> 
  ); 
} 
 

 


js 

CopiaModifica 

export default [ 
  { 
    id: '1', 
    title: 'Spaghetti alla Carbonara', 
    description: 'Ricetta classica con uova, pecorino, guanciale e pepe nero.', 
    ingredients: ['Spaghetti', 'Uova', 'Guanciale', 'Pecorino', 'Pepe nero'], 
    steps: ['Cuoci la pasta', 'Rosola il guanciale', 'Mescola uova e pecorino', 'Unisci tutto e servi'], 
  }, 
  { 
    id: '2', 
    title: 'Pesto alla Genovese', 
    description: 'Salsa fredda a base di basilico, pinoli e parmigiano.', 
    ingredients: ['Basilico', 'Pinoli', 'Aglio', 'Parmigiano', 'Olio EVO'], 
    steps: ['Frulla tutti gli ingredienti', 'Condisci la pasta'], 
  }, 
]; 
 

 


jsx 

CopiaModifica 

import React from 'react'; 
import { TouchableOpacity, Text, StyleSheet } from 'react-native'; 
 
export default function RecipeItem({ recipe, onPress }) { 
  return ( 
    <TouchableOpacity style={styles.item} onPress={onPress}> 
      <Text style={styles.title}>{recipe.title}</Text> 
      <Text>{recipe.description}</Text> 
    </TouchableOpacity> 
  ); 
} 
 
const styles = StyleSheet.create({ 
  item: { 
    padding: 15, 
    marginVertical: 10, 
    backgroundColor: '#f9c2ff', 
    borderRadius: 10, 
  }, 
  title: { 
    fontWeight: 'bold', 
    fontSize: 18, 
  }, 
}); 
 

 


jsx 

CopiaModifica 

import React from 'react'; 
import { FlatList, View } from 'react-native'; 
import RecipeItem from '../components/RecipeItem'; 
import recipes from '../data/recipes'; 
 
export default function HomeScreen({ navigation }) { 
  return ( 
    <View style={{ padding: 20 }}> 
      <FlatList 
        data={recipes} 
        keyExtractor={(item) => item.id} 
        renderItem={({ item }) => ( 
          <RecipeItem 
            recipe={item} 
            onPress={() => navigation.navigate('RecipeDetail', { recipe: item })} 
          /> 
        )} 
      /> 
    </View> 
  ); 
} 
 

 


jsx 

CopiaModifica 

import React from 'react'; 
import { View, Text, StyleSheet } from 'react-native'; 
 
export default function RecipeDetailScreen({ route }) { 
  const { recipe } = route.params; 
 
  return ( 
    <View style={styles.container}> 
      <Text style={styles.title}>{recipe.title}</Text> 
      <Text style={styles.subtitle}>Ingredienti:</Text> 
      {recipe.ingredients.map((ing, idx) => ( 
        <Text key={idx}>• {ing}</Text> 
      ))} 
      <Text style={styles.subtitle}>Procedimento:</Text> 
      {recipe.steps.map((step, idx) => ( 
        <Text key={idx}>{idx + 1}. {step}</Text> 
      ))} 
    </View> 
  ); 
} 
 
const styles = StyleSheet.create({ 
  container: { padding: 20 }, 
  title: { fontSize: 24, fontWeight: 'bold', marginBottom: 10 }, 
  subtitle: { marginTop: 15, fontWeight: 'bold' }, 
}); 
 
