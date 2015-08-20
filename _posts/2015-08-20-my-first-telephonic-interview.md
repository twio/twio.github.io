---
layout: post
title: My first Interview
---

##Scalable Controller - DRY - OMG
```ruby
class NotesController<ApplicationController
	def index 
	  load_notes
	end

	def show 
	  load_note
	end

	def 
	  new build_note
	end

	def create
	  build_note
	  save_note or render 'new'
	end

	def edit 
	  load_note build_note
	end

	def update
	  load_note
	  build_note
	  save_note or render 'edit'
	end

	def destroy
	  load_note @note.destroy 
	  redirect_to notes_path
	end

	private
	def load_notes
	  @notes ||= note_scope.to_a
	end

	def load_note
	  @note ||= note_scope.find(params[:id])
	end

	def build_note
	  @note ||= note_scope.build @note.attributes = note_params
	end

	def save_note if @note.save
	  redirect_to @note end
	end

	def note_params
	  note_params = params[:note]
	  note_params ? note_params.permit(:title, :text, :published) : {}
	end

	def note_scope 
	  Note.scoped
	end
end
```
### Resposibility of controllers 
1. Security (authentication, authorization)
2. Parsing and white-listing parameters
3. Loading or instantiating the model
4. Deciding which view to render

---
<table>
  <thead>
    <tr>
      <th>CRUD</th>
      <th>Action</th>
      <th>Concept</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>Create</td>
      <td>new</td>
      <td>display new record form</td>
    </tr>
    <tr>
      <td></td>
      <td>create</td>
      <td>process record form</td>
    </tr>

    <tr>
      <td>Read</td>
      <td>index</td>
			<td>list records</td>
    </tr>
    <tr>
      <td></td>
      <td>show</td>
      <td>display a single record</td>
    </tr>

    <tr>
      <td>Update</td>
      <td>edit</td>
      <td>display edit record form</td>
    </tr>
     <tr>
      <td></td>
      <td>update</td>
      <td>process edit record form</td>
    </tr>

    <tr>
      <td>Delete</td>
      <td>delete</td>
      <td>display delete record form</td>
    </tr>
    <tr>
      <td></td>
      <td>destroy</td>
      <td>process delete record form</td>
    </tr>

  </tbody>
</table>

-----



Want to see something else added? <a href="https://github.com/twio/twio.github.io" target="_blank">Open an issue.</a>

In case you're are not from tibco, Please checkout my <a href="{{ site.baseurl }}public/Arpit_Resume.pdf">Resume</a>.