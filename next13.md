# How to Nextjs 13

## API Routes

To set up REST Endpoints create `route.ts` files in your app folder path.

E.g. the path /api/foo/:bar has the following folder hierarchy:

- app
- - api
- - - foo
- - - - [bar]
- - - - - route.ts

```ts
export async function PATCH(
	request: Request,
	{ params }: { params: { bar: string } }
) {
	const body = await request.json(); // body contains now { foo: foo }
    const urlParams = params.bar;
	
	return NextResponse.json({
		status: 200,
		message: "Fetched opt in successfully.",
		data: {},
	});
}

export async function DELETE(request: Request) {
	return NextResponse.json({
		status: 200,
		message: "Deleted successfully",
		data: {},
	});
}
```

E.g. with this function you can call a PATCH on the given path:

```ts
export const callPatch = async (foo: string, bar: string) => {
    await axios.patch(`/api/foo/${bar}`, { foo: foo });
};
```
