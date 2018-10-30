# FieldsJS

You don't need a giant framework to submit forms in React. FieldsJS is an ultra-lightweight (1k) helper with zero dependencies. Use plain vanilla HTML form elements or fancier UI components of your choice. Works with React Native too.


## Get started
`npm install fieldsjs --save`

## Docs

### withFormState()
An HOC to wrap your form component. It will provide your form with 4 methods for managing form state

### getFieldValue()
Gets the current value of the field

### setFieldValue()
Sets the value of the field, typically used onChange or onBlur

### submitForm()
Performs the submit action that you have passed into the form component.

### resetForm()
Clears the values of all form elements


## Example
```
import React from 'react';
import { withFieldsjs } from 'fieldsjs';

const ExampleForm = withFormState((props) => {

	const {
		getFieldValue,
		setFieldValue,
		submitForm
	} = props;

	const seasons = [
		"Winter",
		"Spring",
		"Summer",
		"Fall"
	];

	return (
		<form>
			<div>
				<label for="yourname">Your name</label>
				<input
					type="text"
					id="yourname"
					value={getFieldValue('yourname')}
					onChange={ e => setFieldValue('yourname', e.target.value) }
					/>
			</div>
			<div>
				<label for="hometown">Hometown</label>
				<input
					type="text"
					id="hometown"
					value={getFieldValue('hometown')}
					onChange={ e => setFieldValue('hometown', e.target.value) }
					/>
			</div>
			<div>
				<label for="season">Favorite season</label>
				<select
					id="season"
					onChange={ e => setFieldValue('season', e.target.value) }
					>
					{seasons.map((season, i)=>(
						<option
							value={season}
							selected={getFieldValue('season') == season}
							key={i}
							>
							{season}
						</option>
					)}
				</select>
			</div>
			<div>
				<input
					type="button"
					label="Let's do this"
					onPress={ submitForm }
					/>
			</div>
		</form>
	);
});

class ExamplePage extends React.Component {
	static defaultProps = {
		// you'll probably receive values from your redux store
		// but for the demo, we'll manually set them here
	    user: {
	    	yourname: "Sally Formsubmitterson",
	    	hometown: "Clewiston, FL",
	    	season: "Summer"
	    },
	}

	render() {
		<h1>Let's do a form!</h1>
		<p>Isn't it great to be able to do handle React forms without a giant library?</p>
		<TestForm
			initialFields={props.user}
			onSubmit={(fields) => {
				// you'll probably call a redux action here
				// but for the demo, we'll just display our values
				alert(JSON.stringify(fields));
			}}
			/>
	}
}

export default ExamplePage;

```