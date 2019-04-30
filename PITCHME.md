# React Brownbag

---

## Add Some Slide Candy

```jsx
export default function DiskGraph({ instance, capacity, data, live }: Props): JSX.Element {
  const diskLastValueFormatter = React.useCallback(
    (d?: DiskGraphPerfData) => {
      if (d && capacity) {
        return `${formatMBytes(d.UsedMBytes)}/${formatMBytes(capacity)} (${d3.format(",.1%")(d.UsedMBytes / capacity)})`;
      }
      return "No data";
    },
    [capacity]
  );
  const diskDataTransform = React.useCallback(
    (d: VolumePerfData | LiveVolumePerfData) => {
      return {
        ...d,
        UsedMBytes: capacity ? capacity - d.FreeMegabytes : undefined
      } as DiskGraphPerfData;
    },
    [capacity]
  );

  const valueProps = React.useMemo(() => [{ ...usedMBytes, domainMax: capacity }, diskQueueLength], [usedMBytes, capacity, diskQueueLength]);

  return (
    <StatGraph
      label={`Disk space (${instance})`}
      data={data}
      timeProps={timeProps}
      valueProps={valueProps}
      dataTransform={diskDataTransform}
      lastValueFormatter={diskLastValueFormatter}
      color="#498205"
      live={live}
    />
  );
}
```

---
@title[Customize Slide Layout]

@snap[west span-50]
## Customize Slide Content Layout
@snapend

@snap[east span-50]
![](assets/img/presentation.png)
@snapend

---?color=#E58537
@title[Add A Little Imagination]

@snap[north-west]
#### Add a splash of @color[cyan](**color**) and you are ready to start presenting...
@snapend

@snap[west span-55]
@ul[spaced text-white]
- You will be amazed
- What you can achieve
- *With a little imagination...*
- And **GitPitch Markdown**
@ulend
@snapend

@snap[east span-45]
@img[shadow](assets/img/conference.png)
@snapend

---?image=assets/img/presenter.jpg

@snap[north span-100 headline]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
