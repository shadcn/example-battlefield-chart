Source https://twitter.com/MozzyFX/status/1813154329416568966


```tsx
"use client"

import { Bar, BarChart, Rectangle, XAxis, YAxis } from "recharts"

import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from "@/components/ui/card"
import {
  ChartConfig,
  ChartContainer,
  ChartTooltip,
  ChartTooltipContent,
} from "@/components/ui/chart"

const chartData = [
  {
    name: "Battlefield V",
    count: 76986,
    percentage: 34.9,
  },
  {
    name: "Battlefield 2042",
    count: 54713,
    percentage: 24.8,
  },
  {
    name: "Battlefield 4",
    count: 40440,
    percentage: 18.3,
  },
  {
    name: "Battlefield 1",
    count: 35550,
    percentage: 16.1,
  },
  {
    name: "Battlefield 3",
    count: 5612,
    percentage: 2.5,
  },
]

const chartConfig = {
  count: {
    label: "Count",
    color: "hsl(var(--chart-1))",
  },
} satisfies ChartConfig

export function BattleFieldChart() {
  return (
    <Card className="w-full max-w-sm">
      <CardHeader className="pb-2">
        <CardTitle>Per Game</CardTitle>
        <CardDescription>Since May 25, 2011</CardDescription>
      </CardHeader>
      <CardContent>
        <ChartContainer config={chartConfig} className="aspect-[16/11]">
          <BarChart
            accessibilityLayer
            data={chartData}
            layout="vertical"
            barSize={32}
            margin={{
              left: 0,
              right: 0,
            }}
          >
            <YAxis dataKey="name" type="category" hide />
            <XAxis dataKey="count" type="number" hide />
            <Bar
              dataKey="count"
              layout="vertical"
              fill="var(--color-count)"
              background={{ radius: 4, fill: "hsl(var(--muted))" }}
              radius={4}
              shape={(props: any) => (
                <>
                  {/* Draw the bar first. */}
                  <Rectangle {...props} />
                  {/* Places the name at the start */}
                  <text
                    x={props.x + 10}
                    y={props.y + 20}
                    fill="hsl(var(--foreground))"
                  >
                    {props.name}
                  </text>
                  {/* Places the count at the end */}
                  <text
                    x={props.background.width - 10}
                    y={props.y + 20}
                    textAnchor="end"
                    fill="hsl(var(--foreground))"
                  >
                    {props.count.toLocaleString()} (
                    {props.percentage.toFixed(1)}%)
                  </text>
                </>
              )}
            />
            <ChartTooltip
              cursor={false}
              content={<ChartTooltipContent indicator="dot" />}
            />
          </BarChart>
        </ChartContainer>
      </CardContent>
    </Card>
  )
}
```
