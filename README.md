
# React Hooks & Router Guide

## 📚 **React Hook Usage Guide**

#### 📝 **useRef**  
ใช้สำหรับการอ้างอิงถึง DOM หรือค่าที่ไม่ต้องการทำการ re-render เมื่อมีการเปลี่ยนแปลง  
```javascript
const inputRef = useRef(null);
```

#### 🔢 **useState**  
ใช้สำหรับการจัดการกับสถานะ (state) ในคอมโพเนนต์  
```javascript
const [count, setCount] = useState(0);
```

#### 🔄 **useEffect**  
ใช้สำหรับการทำงานบางอย่างเมื่อคอมโพเนนต์ render หรือเมื่อค่าของตัวแปรที่กำหนดเปลี่ยนแปลง  
```javascript
useEffect(() => { console.log('Component mounted'); }, []);
```

#### 🌐 **useQuery**  
ใช้สำหรับการดึงข้อมูลจาก API และจัดการสถานะของข้อมูล (loading, success, error)  
```javascript
const { data, isLoading, error } = useQuery('fetchData', fetchDataFunction);
```

#### 🔧 **useMutation**  
ใช้สำหรับการส่งคำขอที่มีผลกระทบ (POST, PUT, DELETE) และจัดการสถานะการทำงาน  
```javascript
const mutation = useMutation(mutateFunction);
```

#### 🔑 **useParams**  
ใช้สำหรับดึงพารามิเตอร์จาก URL ในการ routing  
```javascript
const { id } = useParams();
```

#### 🌍 **useLocation**  
ใช้สำหรับดึงข้อมูลเกี่ยวกับสถานะของ URL ปัจจุบัน  
```javascript
const location = useLocation();
```

#### 🚀 **useNavigate**  
ใช้สำหรับการนำทางโปรแกรมmatically โดยไม่ต้องใช้ `<Link>` หรือ `<NavLink>`  
```javascript
const navigate = useNavigate();
```

#### 🧩 **useContext**  
ใช้เพื่อดึงข้อมูลจาก Context ใน React (ช่วยในการแชร์ข้อมูลข้ามคอมโพเนนต์)  
```javascript
const value = useContext(MyContext);
```

#### 🏗️ **useReducer**  
ใช้สำหรับการจัดการกับสถานะที่ซับซ้อน โดยใช้ pattern เหมือนกับ Redux  
```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

#### 💡 **useMemo**  
ใช้สำหรับการคำนวณค่าและบันทึกผลลัพธ์ไว้เพื่อหลีกเลี่ยงการคำนวณใหม่ในทุก ๆ การ re-render  
```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

#### 🔁 **useCallback**  
ใช้เพื่อหลีกเลี่ยงการสร้างฟังก์ชันใหม่ในทุก ๆ การ re-render  
```javascript
const memoizedCallback = useCallback(() => { console.log('Memoized callback'); }, []);
```

#### 🔧 **useLayoutEffect**  
คล้ายกับ useEffect แต่จะถูกเรียกใช้หลังจากการ render แต่ก่อนที่ UI จะถูกวาดออกมา  
```javascript
useLayoutEffect(() => { console.log('Layout effect'); }, []);
```

#### 🧳 **useImperativeHandle**  
ใช้สำหรับการกำหนดค่าหรือเมธอดที่สามารถเข้าถึงได้จากคอมโพเนนต์ภายนอกที่ใช้ ref  
```javascript
useImperativeHandle(ref, () => ({ customMethod: () => { console.log('Custom method called'); } }));
```

#### 🛠️ **useDebugValue**  
ใช้สำหรับการเพิ่มค่า debug ให้กับ custom hooks  
```javascript
useDebugValue(value);
```

---

## 🛣️ **React Router**

#### 🚦 **react-router-dom**  
`react-router-dom` ใช้สำหรับการทำ routing ในแอปพลิเคชัน React โดยช่วยให้คุณสามารถสร้างหน้าเว็บหลาย ๆ หน้าและกำหนดเส้นทางการนำทางไปยังหน้าเหล่านั้นได้อย่างง่ายดาย

- **BrowserRouter**: ใช้เพื่อกำหนดการใช้งาน routing ในแอปที่ต้องการการเปลี่ยนแปลง URL  
```javascript
import { BrowserRouter as Router } from 'react-router-dom';
```

- **Route**: ใช้ในการกำหนดเส้นทางไปยังคอมโพเนนต์ต่าง ๆ ในแอปพลิเคชัน  
```javascript
<Route path="/home" component={HomePage} />
```

- **Switch**: ใช้เพื่อทำให้ route ที่ตรงกับ path ที่กำหนดแสดงผล  
```javascript
<Switch>
  <Route path="/home" component={HomePage} />
</Switch>
```

- **Link**: ใช้ในการสร้างลิงก์ที่สามารถคลิกเพื่อเปลี่ยนเส้นทาง  
```javascript
<Link to="/about">About Us</Link>
```

---

## 🧳 **React.lazy()**

#### 💨 **React.lazy()**  
`React.lazy()` ใช้ในการโหลดคอมโพเนนต์แบบ dynamic เมื่อมีการเรียกใช้หรืออยู่ในเส้นทางนั้น ๆ เท่านั้น ช่วยให้ลดขนาดของ bundle file ในการโหลดหน้าเว็บครั้งแรก

- ตัวอย่างการใช้งาน:
```javascript
const LazyComponent = React.lazy(() => import('./LazyComponent'));
```

- การใช้งานร่วมกับ `Suspense`:
```javascript
import React, { Suspense } from 'react';

const LazyComponent = React.lazy(() => import('./LazyComponent'));

const App = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <LazyComponent />
  </Suspense>
);
```

---

### 🚀 **Deployment**
หลังจากที่คุณสร้างแอปพลิเคชัน React พร้อมการใช้งาน `react-router-dom` และ `React.lazy()` เสร็จเรียบร้อยแล้ว, คุณสามารถ deploy แอปพลิเคชันของคุณไปยังเซิร์ฟเวอร์หรือแพลตฟอร์มต่าง ๆ เช่น:

- **Vercel**: สำหรับการ deploy React แอปพลิเคชัน
- **Netlify**: สำหรับการ deploy และ hosting
- **Heroku**: สำหรับการ deploy แอปพลิเคชัน Node.js

