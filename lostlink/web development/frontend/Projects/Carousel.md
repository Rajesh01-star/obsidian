When needed to use hover state on children from hovering over the parent make sure the hover event listener is added on the parent

```js

export default function Card(props) {
  const dur = `${parseInt(props.length / 60)}: ${props.length % 60}`;
  const [hovered, setHovered] = useState(false);
  return (
    <section
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
    >
      <div className={hovered?something:somethingElse}>
        something
      </div>
      <img className=className={hovered?something:somethingElse}>
        src={props.imgUrl}
        alt={props.name}
      />
    </section>
  );
}

```

[project link](https://movie-carousal.vercel.app/)

![screenshot](public/images/2023-05-31_09-54.png)

