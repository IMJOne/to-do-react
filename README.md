![todo-react](https://user-images.githubusercontent.com/110226567/216513282-4e00ce48-80de-467b-9615-ba82ec54d340.png)

# ðï¸ TO-DO LIST (React)

ë¦¬ì¡í¸ ê¸°ë° ë¤í¬ ëª¨ë í¬ëë¦¬ì¤í¸ ð [Demo](https://jone-to-do.netlify.app)

<br />

## ð¢ íë¡ì í¸ ê°ì

ë¦¬ì¡í¸ë¥¼ ê³µë¶íë©´ì ì§íí ì²« ë²ì§¸ íë¡ì í¸, TO-DO LIST ìëë¤.<br />
ë¦¬ì¤í¸ë³ ì§í ìí© íí°ë§ ë° ë¤í¬ ëª¨ë ê¸°ë¥ì´ ìë¡­ê² ì¶ê°ëììµëë¤.

<br />

## ð¨ï¸ ì¬ì© ê¸°ì 

<p>
  <img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=React&logoColor=black"/>
  <img src="https://img.shields.io/badge/PostCSS-DD3A0A?style=flat-square&logo=PostCSS&logoColor=white"/>
</p>

<br />

## ð ì£¼ì ê¸°ë¥

- ë¦¬ì¤í¸ ì¶ê°/ì­ì /ìë£
- ë¦¬ì¤í¸ë³ ìí íí°ë§
- ë¤í¬ ëª¨ë íë§ ì§ì
- ë¡ì»¬ ì¤í ë¦¬ì§ íì©

<br />

## ð» ìì¤ ì½ë

ì ì²´ ì½ë ë³´ë¬ ê°ê¸° ð [Notion](https://imjone.notion.site/React-TO-DO-LIST-bd42d365689243d0b7547d115cefee7b)

### ð ë¦¬ì¤í¸ ì¶ê°

ë¦¬ì¤í¸ë¥¼ ë³´ì¬ì£¼ë ë¡ì§ê³¼, ë¦¬ì¤í¸ë¥¼ ì¶ê°íë ë¡ì§ì ê°ê° ë°ë¡ ë¶ë¦¬í´ì£¼ììµëë¤.<br />
`TodoList` - ë¦¬ì¤í¸ë¥¼ UIì íê¸°íë ìµìì ì»´í¬ëí¸ë¡, ì ì²´ ë¦¬ì¤í¸ ë°°ì´ì ìíë¥¼ ê´ë¦¬í©ëë¤.<br />
`AddTodo` - `props`ë¡ ë°ì `onAdd` ì½ë°±í¨ìë¥¼ í¸ì¶íì¬ ìë¡­ê² ì¶ê°ë ë¦¬ì¤í¸ë¥¼ ì¸ìë¡ ì ë¬í©ëë¤.

```javascript
export default function TodoList() {
  const [todos, setTodos] = useState([]);
  const handleAdd = todo => setTodos([...todos, todo])};

  return (
    <section>
      <ul>{todos.map(item => (<li key={item.id}>{item.text}</li>))}</ul>
      <AddTodo onAdd={handleAdd} />
    </section>
  );
}
```
```javascript
export default function AddTodo({ onAdd }) {
  const [text, setText] = useState('');
  const handleChange = e => setText(e.target.value);
  const handleSubmit = e => {
    e.preventDefault();
    if (text.trim().length === 0) return;
    onAdd({ id: uuidv4(), text, status: 'active' });
    setText(''); // ìë ¥ê° ì´ê¸°í
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="add Todo" value={text} onChange={handleChange} />
      <button type="submit">Add</button>
    </form>
  );
}
```

### ð íí°ë§ ì ì©

íí°ë§ ëª©ë¡ì ë°°ì´ë¡ ì ìí´ëê³ , `useState`ë¥¼ íµí´ íì¬ íí°ê°ì ìíë¥¼ ê´ë¦¬í©ëë¤.<br />
ìì ì»´í¬ëí¸ìê² íí°ë§ì íìí ì ë³´ë¤ì ê°ê° `props`ë¡ ì ë¬íì¬ ì ì íê² ìíë¥¼ ìë°ì´í¸í©ëë¤.

```javascript
const filters = ['all', 'active', 'completed'];
export default function App() {
  const [filter, setFilter] = useState(filters[0]);

  return (
    <div>
      <Header filters={filters} filter={filter} onFilterChange={setFilter} />
      <TodoList filter={filter} />
    </div>
  );
}
```

### ð ë¤í¬ ëª¨ë êµ¬í

ë¤í¬ëª¨ëë ì ì­ì ì¸ ë°ì´í°ì ì±ê²©ì ëê³  ìê¸° ëë¬¸ì Contextë¥¼ íµí´ ê´ë¦¬í©ëë¤.<br />
íì¬ ëª¨ë ìíì ëª¨ëë¥¼ í ê¸ë§í  ì ìë í¨ìë¥¼ ë§ë  í Providerì `value`ë¡ ì ë¬í´ì£¼ê³ ,<br />
ì»´í¬ëí¸ê° ì²ì mount ë  ë ë¡ì»¬ ì¤í ë¦¬ì§ì ì ì¥ë íì¬ íë§ ì¤ì ì´ ê·¸ëë¡ ì ì©ëê²ë êµ¬ííììµëë¤.

```javascript
const DarkModeContext = createContext();
function updateDarkMode(darkMode) {
  if (darkMode) {
    document.documentElement.classList.add('dark');
    localStorage.theme = 'dark';
  } else {
    document.documentElement.classList.remove('dark');
    localStorage.theme = 'light';
  }
}

export function DarkModeProvider({ children }) {
  const [darkMode, setDarkMode] = useState(false);

  const toggleDarkMode = () => {
    setDarkMode(!darkMode);
    updateDarkMode(!darkMode);
  };

  useEffect(() => {
    const isDarkMode = localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches);
    setDarkMode(isDarkMode);
    updateDarkMode(isDarkMode);
  }, []);

  return <DarkModeContext.Provider value={{ darkMode, toggleDarkMode }}>{children}</DarkModeContext.Provider>;
}

// ì»¤ì¤í í
export const useDarkMode = () => useContext(DarkModeContext);
```

<br />

## ð ë°°ì´ ì  ë° ëë ì 

- ë¦¬ì¡í¸ ì´íë¦¬ì¼ì´ìì ì ë°ì ì¸ íë¦ì ì´í´í  ì ìììµëë¤.
- ì»´í¬ëí¸ì ìíë¥¼ ì´ë¤ ìì¼ë¡ ìë°ì´í¸íì¬ UIì ë°ìí  ì ìëì§ ìë¦¬ì ëí´ ìê² ëììµëë¤.
- ë¦¬ì¡í¸ì ë¨ë°©í¥ ë°ì´í° íë¦ê³¼ ì­ë°©í¥ ì´ë²¤í¸ íë¦, ìí ëì´ì¬ë¦¬ê¸°ì ëí ê°ëì ë ê³µë¶í´ì¼ê² ë¤ê³  ëê¼ìµëë¤.
