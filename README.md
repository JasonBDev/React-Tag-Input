### React Tag Input Component by JasonBDev

- Easy to use React component that uses React Hooks such as useState.
- Uses TailwindCSS for styling.
- Automatically deletes last tag with Backspace.
- Each tag has a button to remove the tag.
- Each tag is its own object with ID and Value.

![alt text](https://prnt.sc/26bdn50)

```javascript
import Head from 'next/head'
import Image from 'next/image'
import styles from '../styles/Home.module.css'
import { useState, useEffect } from 'react'

export default function Home() {

  const [input, setInput] = useState('');
  const [tags, setTags] = useState([]);

  useEffect(() => {
    console.log(tags);
  }, [tags])

  return (
    <div className='p-16'>

      <div className="max-w-xl border border-gray-300 rounded-md">
        <div className="flex flex-row flex-wrap p-2 border w-full">

          {tags.map((value, index) => {
            return (
              <div key={index} className="flex flex-row items-center bg-gray-200 px-3 mr-1 my-1 rounded-xl">
                <h1 className='font-medium text-sm'>{value.value}</h1>
                <button className='ml-2' onClick={() => {
                  const arr = [...tags];
                  arr.splice(index, 1);
                  setTags(arr);
                }}>
                  <svg xmlns="http://www.w3.org/2000/svg" className="h-4 w-4 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
                  </svg>
                </button>
              </div>
            )
          })}

          <input onKeyDown={(e) => {
            if (e.key == 'Enter') {
              setTags([...tags, {
                id: tags.length,
                value: input,
              }])
              setInput('');
            } else if (e.key == 'Backspace' && input == '') {
              const arr = [...tags];
              arr.pop();
              setTags(arr);
            }
          }} onChange={(e) => {
            setInput(e.target.value);
          }} value={input} placeholder='Search..' className='focus:outline-none ml-2' />
        </div>
      </div>
    </div>
  )
}

```
