# Context API
## How to Setup Context API Store
- src/Context/Cart.jsx
```
import { createContext, useContext, useState } from "react";
import PropTypes from "prop-types";



const Mycontext = createContext();



export const CartProvider = ({children}) => {
  const [cart, setCart] = useState({
    name: '',
    age: null
  })

  

  return (
    <>
       <Mycontext.Provider value={[cart, setCart]}>
            {children}
       </Mycontext.Provider>
    </>
  )
}



// PropTypes validation for the 'children' prop
CartProvider.propTypes = {
  children: PropTypes.node.isRequired,
};



// Custom Hook
export const  useCart = () => useContext(Mycontext);
```

## How to provide the Context API store to React
- src/main.jsx
```
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import { CartProvider } from './Context/Cart.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <CartProvider>
      <App />
      </CartProvider>
  </StrictMode>,
)
```
## Create components
- src/app.jsx
```
import { useCart } from "./Context/Cart"


const App = () => {

   const [cart, setCart] = useCart();

  return (
    <div>
      <button onClick={()=>setCart({...cart, name:'Ahmad', age:17})}>Press</button>
     <h1>My name is {cart.name}</h1>
     <h1>My age is {cart.age}</h1>

    </div>
  )
}

export default App
```
