# FieldsJS

You don't need a giant framework to submit forms in React. FieldsJS is an ultra-lightweight (1k) helper with zero dependencies. Use plain vanilla HTML form elements or fancier UI components of your choice. Works with React Native too.


## Get started
`npm install fieldsjs --save`

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
					{(["Winter", "Spring", "Summer", "Fall"]).map((season, i)=>(
						<option
							value="{season}"
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