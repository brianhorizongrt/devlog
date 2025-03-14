---
title: "Grid Row - Col [Ref: https://ant.design/components/grid]"
date: "01.01.2025"
---

Row and col using css module, a lightweight and efficient solution without using Antd, I just created some basic props
&nbsp;

Row.tsx
```typescript
import React from "react";

import s from "./grid.module.css";

type RowProps = {
	children: React.ReactNode;
	gutter?: [number, number];
};

export const Row = ({ children, gutter = [0, 0] }: RowProps) => {
	const [horizontal, vertical] = gutter;

	return (
		<div
			className={s.row}
			style={{
				marginInline: -horizontal / 2,
				rowGap: vertical,
			}}
		>
			{React.Children.map(children, (child) => {
				if (!React.isValidElement(child)) return child;
				return React.cloneElement(child, {
					...child.props,
					style: {
						...child.props.style,
						paddingInline: horizontal / 2,
					},
				});
			})}
		</div>
	);
};
```

&nbsp;

Col.tsx
```typescript
import React from "react";

import s from "./grid.module.css";

type ColProps = {
	children?: React.ReactNode;
	xs?: number;
	sm?: number;
	md?: number;
	lg?: number;
	xl?: number;
	xxl?: number;
} & Omit<React.HTMLAttributes<HTMLDivElement>, "children">;

const sizes = ["xs", "sm", "md", "lg", "xl", "xxl"] as const;

export const Col = ({ children, xs = 24, sm, md, lg, xl, xxl, ...props }: ColProps) => {
	const getValueForBreakpoint = (breakpointIndex: number): number | undefined => {
		for (let i = breakpointIndex; i >= 0; i--) {
			const size = sizes[i];
			const value = size === "xs" ? xs : { sm, md, lg, xl, xxl }[size];
			if (value !== undefined && value >= 0 && value <= 24) {
				return value;
			}
		}
		return undefined;
	};

	const sizeClasses = sizes
		.map((size, index) => {
			const value = getValueForBreakpoint(index);
			if (value === undefined) return "";
			return s[`col-${size}-${value}`];
		})
		.filter(Boolean)
		.join(" ");

	return (
		<div className={`${s.col} ${sizeClasses}`.trim()} {...props}>
			{children}
		</div>
	);
};
```

&nbsp;

grid.module.css
```typescript
.row {
	display: flex;
	flex-flow: row wrap;
	box-sizing: border-box;
}

.col {
	position: relative;
	max-width: 100%;
	box-sizing: border-box;
}

/* Generate columns for different breakpoints */
@media (max-width: 575px) {
	.col-xs-24 {
		flex: 0 0 100%;
		max-width: 100%;
	}
	.col-xs-23 {
		flex: 0 0 95.833333%;
		max-width: 95.833333%;
	}
	.col-xs-22 {
		flex: 0 0 91.666667%;
		max-width: 91.666667%;
	}
	.col-xs-21 {
		flex: 0 0 87.5%;
		max-width: 87.5%;
	}
	.col-xs-20 {
		flex: 0 0 83.333333%;
		max-width: 83.333333%;
	}
	.col-xs-19 {
		flex: 0 0 79.166667%;
		max-width: 79.166667%;
	}
	.col-xs-18 {
		flex: 0 0 75%;
		max-width: 75%;
	}
	.col-xs-17 {
		flex: 0 0 70.833333%;
		max-width: 70.833333%;
	}
	.col-xs-16 {
		flex: 0 0 66.666667%;
		max-width: 66.666667%;
	}
	.col-xs-15 {
		flex: 0 0 62.5%;
		max-width: 62.5%;
	}
	.col-xs-14 {
		flex: 0 0 58.333333%;
		max-width: 58.333333%;
	}
	.col-xs-13 {
		flex: 0 0 54.166667%;
		max-width: 54.166667%;
	}
	.col-xs-12 {
		flex: 0 0 50%;
		max-width: 50%;
	}
	.col-xs-11 {
		flex: 0 0 45.833333%;
		max-width: 45.833333%;
	}
	.col-xs-10 {
		flex: 0 0 41.666667%;
		max-width: 41.666667%;
	}
	.col-xs-9 {
		flex: 0 0 37.5%;
		max-width: 37.5%;
	}
	.col-xs-8 {
		flex: 0 0 33.333333%;
		max-width: 33.333333%;
	}
	.col-xs-7 {
		flex: 0 0 29.166667%;
		max-width: 29.166667%;
	}
	.col-xs-6 {
		flex: 0 0 25%;
		max-width: 25%;
	}
	.col-xs-5 {
		flex: 0 0 20.833333%;
		max-width: 20.833333%;
	}
	.col-xs-4 {
		flex: 0 0 16.666667%;
		max-width: 16.666667%;
	}
	.col-xs-3 {
		flex: 0 0 12.5%;
		max-width: 12.5%;
	}
	.col-xs-2 {
		flex: 0 0 8.333333%;
		max-width: 8.333333%;
	}
	.col-xs-1 {
		flex: 0 0 4.166667%;
		max-width: 4.166667%;
	}
}

@media (min-width: 576px) {
	.col-sm-24 {
		flex: 0 0 100%;
		max-width: 100%;
	}
	.col-sm-23 {
		flex: 0 0 95.833333%;
		max-width: 95.833333%;
	}
	.col-sm-22 {
		flex: 0 0 91.666667%;
		max-width: 91.666667%;
	}
	.col-sm-21 {
		flex: 0 0 87.5%;
		max-width: 87.5%;
	}
	.col-sm-20 {
		flex: 0 0 83.333333%;
		max-width: 83.333333%;
	}
	.col-sm-19 {
		flex: 0 0 79.166667%;
		max-width: 79.166667%;
	}
	.col-sm-18 {
		flex: 0 0 75%;
		max-width: 75%;
	}
	.col-sm-17 {
		flex: 0 0 70.833333%;
		max-width: 70.833333%;
	}
	.col-sm-16 {
		flex: 0 0 66.666667%;
		max-width: 66.666667%;
	}
	.col-sm-15 {
		flex: 0 0 62.5%;
		max-width: 62.5%;
	}
	.col-sm-14 {
		flex: 0 0 58.333333%;
		max-width: 58.333333%;
	}
	.col-sm-13 {
		flex: 0 0 54.166667%;
		max-width: 54.166667%;
	}
	.col-sm-12 {
		flex: 0 0 50%;
		max-width: 50%;
	}
	.col-sm-11 {
		flex: 0 0 45.833333%;
		max-width: 45.833333%;
	}
	.col-sm-10 {
		flex: 0 0 41.666667%;
		max-width: 41.666667%;
	}
	.col-sm-9 {
		flex: 0 0 37.5%;
		max-width: 37.5%;
	}
	.col-sm-8 {
		flex: 0 0 33.333333%;
		max-width: 33.333333%;
	}
	.col-sm-7 {
		flex: 0 0 29.166667%;
		max-width: 29.166667%;
	}
	.col-sm-6 {
		flex: 0 0 25%;
		max-width: 25%;
	}
	.col-sm-5 {
		flex: 0 0 20.833333%;
		max-width: 20.833333%;
	}
	.col-sm-4 {
		flex: 0 0 16.666667%;
		max-width: 16.666667%;
	}
	.col-sm-3 {
		flex: 0 0 12.5%;
		max-width: 12.5%;
	}
	.col-sm-2 {
		flex: 0 0 8.333333%;
		max-width: 8.333333%;
	}
	.col-sm-1 {
		flex: 0 0 4.166667%;
		max-width: 4.166667%;
	}
}

@media (min-width: 768px) {
	.col-md-24 {
		flex: 0 0 100%;
		max-width: 100%;
	}
	.col-md-23 {
		flex: 0 0 95.833333%;
		max-width: 95.833333%;
	}
	.col-md-22 {
		flex: 0 0 91.666667%;
		max-width: 91.666667%;
	}
	.col-md-21 {
		flex: 0 0 87.5%;
		max-width: 87.5%;
	}
	.col-md-20 {
		flex: 0 0 83.333333%;
		max-width: 83.333333%;
	}
	.col-md-19 {
		flex: 0 0 79.166667%;
		max-width: 79.166667%;
	}
	.col-md-18 {
		flex: 0 0 75%;
		max-width: 75%;
	}
	.col-md-17 {
		flex: 0 0 70.833333%;
		max-width: 70.833333%;
	}
	.col-md-16 {
		flex: 0 0 66.666667%;
		max-width: 66.666667%;
	}
	.col-md-15 {
		flex: 0 0 62.5%;
		max-width: 62.5%;
	}
	.col-md-14 {
		flex: 0 0 58.333333%;
		max-width: 58.333333%;
	}
	.col-md-13 {
		flex: 0 0 54.166667%;
		max-width: 54.166667%;
	}
	.col-md-12 {
		flex: 0 0 50%;
		max-width: 50%;
	}
	.col-md-11 {
		flex: 0 0 45.833333%;
		max-width: 45.833333%;
	}
	.col-md-10 {
		flex: 0 0 41.666667%;
		max-width: 41.666667%;
	}
	.col-md-9 {
		flex: 0 0 37.5%;
		max-width: 37.5%;
	}
	.col-md-8 {
		flex: 0 0 33.333333%;
		max-width: 33.333333%;
	}
	.col-md-7 {
		flex: 0 0 29.166667%;
		max-width: 29.166667%;
	}
	.col-md-6 {
		flex: 0 0 25%;
		max-width: 25%;
	}
	.col-md-5 {
		flex: 0 0 20.833333%;
		max-width: 20.833333%;
	}
	.col-md-4 {
		flex: 0 0 16.666667%;
		max-width: 16.666667%;
	}
	.col-md-3 {
		flex: 0 0 12.5%;
		max-width: 12.5%;
	}
	.col-md-2 {
		flex: 0 0 8.333333%;
		max-width: 8.333333%;
	}
	.col-md-1 {
		flex: 0 0 4.166667%;
		max-width: 4.166667%;
	}
}

@media (min-width: 992px) {
	.col-lg-24 {
		flex: 0 0 100%;
		max-width: 100%;
	}
	.col-lg-23 {
		flex: 0 0 95.833333%;
		max-width: 95.833333%;
	}
	.col-lg-22 {
		flex: 0 0 91.666667%;
		max-width: 91.666667%;
	}
	.col-lg-21 {
		flex: 0 0 87.5%;
		max-width: 87.5%;
	}
	.col-lg-20 {
		flex: 0 0 83.333333%;
		max-width: 83.333333%;
	}
	.col-lg-19 {
		flex: 0 0 79.166667%;
		max-width: 79.166667%;
	}
	.col-lg-18 {
		flex: 0 0 75%;
		max-width: 75%;
	}
	.col-lg-17 {
		flex: 0 0 70.833333%;
		max-width: 70.833333%;
	}
	.col-lg-16 {
		flex: 0 0 66.666667%;
		max-width: 66.666667%;
	}
	.col-lg-15 {
		flex: 0 0 62.5%;
		max-width: 62.5%;
	}
	.col-lg-14 {
		flex: 0 0 58.333333%;
		max-width: 58.333333%;
	}
	.col-lg-13 {
		flex: 0 0 54.166667%;
		max-width: 54.166667%;
	}
	.col-lg-12 {
		flex: 0 0 50%;
		max-width: 50%;
	}
	.col-lg-11 {
		flex: 0 0 45.833333%;
		max-width: 45.833333%;
	}
	.col-lg-10 {
		flex: 0 0 41.666667%;
		max-width: 41.666667%;
	}
	.col-lg-9 {
		flex: 0 0 37.5%;
		max-width: 37.5%;
	}
	.col-lg-8 {
		flex: 0 0 33.333333%;
		max-width: 33.333333%;
	}
	.col-lg-7 {
		flex: 0 0 29.166667%;
		max-width: 29.166667%;
	}
	.col-lg-6 {
		flex: 0 0 25%;
		max-width: 25%;
	}
	.col-lg-5 {
		flex: 0 0 20.833333%;
		max-width: 20.833333%;
	}
	.col-lg-4 {
		flex: 0 0 16.666667%;
		max-width: 16.666667%;
	}
	.col-lg-3 {
		flex: 0 0 12.5%;
		max-width: 12.5%;
	}
	.col-lg-2 {
		flex: 0 0 8.333333%;
		max-width: 8.333333%;
	}
	.col-lg-1 {
		flex: 0 0 4.166667%;
		max-width: 4.166667%;
	}
}

@media (min-width: 1200px) {
	.col-xl-24 {
		flex: 0 0 100%;
		max-width: 100%;
	}
	.col-xl-23 {
		flex: 0 0 95.833333%;
		max-width: 95.833333%;
	}
	.col-xl-22 {
		flex: 0 0 91.666667%;
		max-width: 91.666667%;
	}
	.col-xl-21 {
		flex: 0 0 87.5%;
		max-width: 87.5%;
	}
	.col-xl-20 {
		flex: 0 0 83.333333%;
		max-width: 83.333333%;
	}
	.col-xl-19 {
		flex: 0 0 79.166667%;
		max-width: 79.166667%;
	}
	.col-xl-18 {
		flex: 0 0 75%;
		max-width: 75%;
	}
	.col-xl-17 {
		flex: 0 0 70.833333%;
		max-width: 70.833333%;
	}
	.col-xl-16 {
		flex: 0 0 66.666667%;
		max-width: 66.666667%;
	}
	.col-xl-15 {
		flex: 0 0 62.5%;
		max-width: 62.5%;
	}
	.col-xl-14 {
		flex: 0 0 58.333333%;
		max-width: 58.333333%;
	}
	.col-xl-13 {
		flex: 0 0 54.166667%;
		max-width: 54.166667%;
	}
	.col-xl-12 {
		flex: 0 0 50%;
		max-width: 50%;
	}
	.col-xl-11 {
		flex: 0 0 45.833333%;
		max-width: 45.833333%;
	}
	.col-xl-10 {
		flex: 0 0 41.666667%;
		max-width: 41.666667%;
	}
	.col-xl-9 {
		flex: 0 0 37.5%;
		max-width: 37.5%;
	}
	.col-xl-8 {
		flex: 0 0 33.333333%;
		max-width: 33.333333%;
	}
	.col-xl-7 {
		flex: 0 0 29.166667%;
		max-width: 29.166667%;
	}
	.col-xl-6 {
		flex: 0 0 25%;
		max-width: 25%;
	}
	.col-xl-5 {
		flex: 0 0 20.833333%;
		max-width: 20.833333%;
	}
	.col-xl-4 {
		flex: 0 0 16.666667%;
		max-width: 16.666667%;
	}
	.col-xl-3 {
		flex: 0 0 12.5%;
		max-width: 12.5%;
	}
	.col-xl-2 {
		flex: 0 0 8.333333%;
		max-width: 8.333333%;
	}
	.col-xl-1 {
		flex: 0 0 4.166667%;
		max-width: 4.166667%;
	}
}

@media (min-width: 1600px) {
	.col-xxl-24 {
		flex: 0 0 100%;
		max-width: 100%;
	}
	.col-xxl-23 {
		flex: 0 0 95.833333%;
		max-width: 95.833333%;
	}
	.col-xxl-22 {
		flex: 0 0 91.666667%;
		max-width: 91.666667%;
	}
	.col-xxl-21 {
		flex: 0 0 87.5%;
		max-width: 87.5%;
	}
	.col-xxl-20 {
		flex: 0 0 83.333333%;
		max-width: 83.333333%;
	}
	.col-xxl-19 {
		flex: 0 0 79.166667%;
		max-width: 79.166667%;
	}
	.col-xxl-18 {
		flex: 0 0 75%;
		max-width: 75%;
	}
	.col-xxl-17 {
		flex: 0 0 70.833333%;
		max-width: 70.833333%;
	}
	.col-xxl-16 {
		flex: 0 0 66.666667%;
		max-width: 66.666667%;
	}
	.col-xxl-15 {
		flex: 0 0 62.5%;
		max-width: 62.5%;
	}
	.col-xxl-14 {
		flex: 0 0 58.333333%;
		max-width: 58.333333%;
	}
	.col-xxl-13 {
		flex: 0 0 54.166667%;
		max-width: 54.166667%;
	}
	.col-xxl-12 {
		flex: 0 0 50%;
		max-width: 50%;
	}
	.col-xxl-11 {
		flex: 0 0 45.833333%;
		max-width: 45.833333%;
	}
	.col-xxl-10 {
		flex: 0 0 41.666667%;
		max-width: 41.666667%;
	}
	.col-xxl-9 {
		flex: 0 0 37.5%;
		max-width: 37.5%;
	}
	.col-xxl-8 {
		flex: 0 0 33.333333%;
		max-width: 33.333333%;
	}
	.col-xxl-7 {
		flex: 0 0 29.166667%;
		max-width: 29.166667%;
	}
	.col-xxl-6 {
		flex: 0 0 25%;
		max-width: 25%;
	}
	.col-xxl-5 {
		flex: 0 0 20.833333%;
		max-width: 20.833333%;
	}
	.col-xxl-4 {
		flex: 0 0 16.666667%;
		max-width: 16.666667%;
	}
	.col-xxl-3 {
		flex: 0 0 12.5%;
		max-width: 12.5%;
	}
	.col-xxl-2 {
		flex: 0 0 8.333333%;
		max-width: 8.333333%;
	}
	.col-xxl-1 {
		flex: 0 0 4.166667%;
		max-width: 4.166667%;
	}
}
```
