# SpringHibernateMaven

<%@page import="com.sun.xml.internal.txw2.Document"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ page isELIgnored="false"%>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="spring" uri="http://www.springframework.org/tags"%>


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet"
	href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">
<script
	src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"
	type="text/javascript"></script>
<script
	src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js"
	type="text/javascript"></script>
<script
	src="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js"
	type="text/javascript"></script>
<script type="text/javascript"
	src="https://code.jquery.com/jquery-3.3.1.js"></script>

<script type="text/javascript"
	src="https://cdn.datatables.net/1.10.19/js/jquery.dataTables.min.js"></script>
<script type="text/javascript"
	src="https://cdn.datatables.net/1.10.19/js/dataTables.bootstrap4.min.js"></script>

</head>
<script type="text/javascript">
	$(document).ready(function() {
		$('.dtVerticalScroll').DataTable({
			"scrollY" : "50vh",
			"scrollCollapse" : true,
			"info":false
		});
		$('.dataTables_length').addClass('bs-select');
	});
</script>

<script>
function copyFunction() {
    if (confirm("Do you really want to copy the selected item?")) {
        
    } else {
        
    }
    document.getElementById("copy").innerHTML;
}
</script>
<!-- <script>
function deleteFunction() {
    if (confirm("Do you really want to delete the selected item?")) {
        
    } else {
    }
    document.getElementById("delete").innerHTML;
} 
</script> -->
<style>
.bgcolor{
	background-color:#A0CFEC;
}
.btn{
	background-color:#77BFC7;
}
</style> 
<body>
	<form:form method="POST" modelAttribute="ucm" action="" id="catForm" name="ucm">

		<div class="container">
		
		
			<h2 class="text-center"><u>List Of Categories</u></h2><br>
			<table  class="dtVerticalScroll table  table-hover table-striped table-bordered table-sm" style="background-color:#F0F8FF">
				<thead class="bgcolor">
					<tr>
						<th class="th-sm">Category<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">CUG<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Active<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">No.Of Events<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Select<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					<c:forEach items="${categories}" var="categ" varStatus="status">
						<tr>
                                         		<td class="titelClass"> ${categ.titel}</td>
                                         		<td>${categ.hasClosedUserGroup}</td>
                                         		<td class="activeState">${categ.activeState}</td>
                                         		<td>${categ.anzEvents}</td>
                                         		 <td>${categ.idrow}</td> 
                                               <td><form:radiobutton path="idrow" value="${categ.idrow}"  />
                                                </td> 
					</c:forEach>
				</tbody>
			</table><br>
			<div class="container-fluid">
			<div class="row">
			<div class="col text-center">
			<button type="button" class="btn" data-toggle="modal" data-target="#editModal" onclick="editBox();">Edit</button>
			<button type="button" class="btn" onclick="copyFunction()">Copy</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#DeleteModal">Delete</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#perModal" name="categPermButton">Permission</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#uplModal">Upload</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#regModal" name="regButton">Registration</button>
			<button type="button" class="btn btn-show-value" data-toggle="modal" data-target="#urlModal"  >URL</button>
			<button type="button" class="btn" data-toggle="modal" data-target="#newModal">New</button>
			</div>
			</div>
		</div>
		<!-- Edit Modal -->
  <div class="modal fade" id="editModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Category Properties</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
         <form action="/action_page.php">
    <div class="form-group">
      <label for="name">Name Of Category:</label>
      <form:input path="titel" cssClass="form-control"/>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio1">Activation State:
       <%--  <form:radiobutton path="idrow"  class="form-check-input" id="radio1" name="optradio" value="yes" />On --%>
       <input type='radio' name='optradio' value='yes' />On
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio2">
       <!--  <input type="radio" class="form-check-input" id="radio2" name="optradio">Off -->
       <form:radiobutton path="idrow" class="form-check-input" id="radio2"  value="${categ.idrow}" />Off
      </label>
    </div><br><br>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio3">Visible In The List:
        <form:radiobutton path="code"  class="form-check-input" id="radio3" name="optradio1" value="${categ.code}" />Visible
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio4">
        <form:radiobutton path="code"  class="form-check-input" id="radio4" name="optradio1" value="${categ.code}"/>Not Visible
      </label>
    </div><br><br>
    <div class="form-group">
      <label for="name">Registration:</label>
      <img src="<c:url value="/static/de.gif"/>" >
      <img src="<c:url value="/static/en.gif" />" >				 				
      <img src="<c:url value="/static/fr.gif" /> " >
      <img src="<c:url value="/static/it.gif" /> " >
    </div>
  </form>
        </div>
        <div class="modal-footer">
          <button type="submit" class="btn"  onclick='this.form.action="save/";'>Save</button>
        </div>
      </div>
    </div>
  </div>

  <script>
  function editBox(){
	  
	  var radio = document.getElementsByName('idrow');
	  var titel=document.getElementsByClassName('titelClass');
	  var active= document.getElementsByClassName('activeState');
	  var rBox="";
	  var inputBox="";
	 
	  for(var i = 0; i < radio.length; i++){
	      if(radio[i].checked){
	          inputBox = titel[i].innerHTML;
	          rBox= active[i].innerHTML;
	       
	      }
	  }
	  document.getElementById("titel").value=inputBox;
	  document.getElementById("titel").autofocus="autofocus";

	  if(rBox=="yes"){
		  document.getElementById("idrow").value=rBox;
		  alert(idrow);
	  }
	  $(function() {
		    var $radios = $('input:radio[name=optradio]');
		    if($radios.is(':checked') === false) {
		        $radios.filter('[value=yes]').prop('checked', true);
		        alert(radios);
		    }
		});
  } 
  </script>
  <script type="text/javascript">
  
  </script>
  
  <!-- Copy Button-->
  <p id="copy"></p>
  <!-- Copy Button -->
  
  <!-- Delete Button-->
  <!-- <p id="delete"></p> -->
  
  <div class="modal fade" id="DeleteModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        <!-- Modal Header -->
        <div class="modal-header">
          <h4 class="modal-title">Category Delete</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        <!-- Modal body -->
        <div class="modal-body">
         Are you sure you want to delete?
        </div>
        
        <!-- Modal footer -->
        <div class="modal-footer">
          <button type="submit" class="btn"  onclick='this.form.action="cd/";'>OK</button>
        </div>
        
      </div>
    </div>
  </div>
  
  <!-- Delete Button -->
  
  <!-- Permission Modal -->
  <div class="modal fade" id="perModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Category Permission</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
         <div class="container-fluid">
		<div class="row">
		<div class="col text-center">
			<h5 class="text-center">Category Managers</h5><br>
			<table id="dtVerticalScroll1" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<th class="th-sm">GPN<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Select<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					
				</tbody>
			</table></div></div></div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal" onclick="deleteFunction()">Delete</button>
          <button type="button" class="btn" data-dismiss="modal" data-toggle="modal" data-target="#pernewModal">New</button>
        </div>
      </div>
    </div>
  </div>
  
  <div class="modal fade" id="pernewModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
       
        <div class="modal-header">
          <h4 class="modal-title">User Search</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        
        <div class="modal-body">
          <div class="form-group">
      <label for="name">Last Name:</label>
      <input type="text" class="form-control" id="lname" name="name">
    </div>
    <div class="form-group">
      <label for="name">First Name:</label>
      <input type="text" class="form-control" id="fname" name="name">
    </div>
    <div class="form-group">
      <label for="name">GPN:</label>
      <input type="text" class="form-control" id="gpn" name="gpn">
    </div>
        </div>
        
        
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Search</button>
          <button type="button" class="btn" data-dismiss="modal">Reset</button>
        </div>
        
      </div>
    </div>
  </div>
  <!-- Permission Modal -->
  
   <!-- Upload Modal -->
   
    <div class="modal fade" id="uplModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">List Of Categories</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
          <div class="container">
 
  <ul class="nav nav-pills" role="tablist">
    <li class="nav-item">
      <a class="nav-link active" data-toggle="pill" href="#user">User Group</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" data-toggle="pill" href="#ban">Banner</a>
    </li>
  </ul>

  
  <div class="tab-content">
    <div id="user" class="container tab-pane active"><br>
      <h5>Upload Closed User Group</h5>
      <div class="container mt-3">
  <form action="/action_page.php">
    File Name:
    <div class="custom-file mb-3">
      <input type="file" class="custom-file-input" id="filename" name="filename">
      <label class="custom-file-label" for="filename">Choose file</label>
    </div>  
    <div class="mt-3">
      <button type="submit" class="btn">Upload</button>
    </div><br>
    <div class="row">
    <div class="col-4">
            Level:
            <select class="custom-select" id="level">
                <option value=""></option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div>
        <div class="col-4">
            Feedback:
            <select class="custom-select" id="feedback">
                <option value=""></option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div></div><br>
        <h6 class="text-center">Closed User Group List</h6>
        <table id="dtVerticalScroll" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<th class="th-sm">GPN<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Email<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Location<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Level<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Feedback<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Language<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					<c:forEach items="${areas}" var="area" varStatus="status">
						<tr>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
						</tr>
					</c:forEach>
				</tbody>
			</table>
  </form>
</div>
    </div>
    <div id="ban" class="container tab-pane fade"><br>
      <h5>Upload Banner</h5>
      <div class="container mt-3">
  <form action="/action_page.php">
    File Name:
    <div class="custom-file mb-3">
      <input type="file" class="custom-file-input" id="file" name="filename">
      <label class="custom-file-label" for="file">Choose file</label>
    </div>
    <div class="row">
    <div class="col-4">
            Language:
            <select class="custom-select" id="lang">
                <option value=""></option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div></div>  
    <div class="mt-3">
      <button type="submit" class="btn">Upload</button>
      <button type="submit" class="btn">Default Banner</button>
    </div><br><br>
        <h6 class="text-center">Banner List</h6>
        <table id="dtVerticalScroll" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<th class="th-sm">File Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Language<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Level<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					<c:forEach items="${areas}" var="area" varStatus="status">
						<tr>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
						</tr>
					</c:forEach>
				</tbody>
			</table>
  </form>
</div>
    </div>
  </div>
</div>
           
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Show</button>
          <button type="button" class="btn" data-dismiss="modal">Excel Export</button>
          <button type="button" class="btn" data-dismiss="modal">Delete</button>
          <button type="button" class="btn" data-dismiss="modal">Delete List</button>
        </div>
        
      </div>
    </div>
  </div></div>
    <!-- Upload Modal -->
    
     <!-- Registration Modal -->
    <div class="modal fade" id="regModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Registration</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        
        <div class="modal-body">
         <h5>Search</h5>
          <div class="row">
           <div class="col-11">
           Event:
            <select class="custom-select" path="event" id="event" >
              <%--  <form:option value="ALL"></form:option> --%>
            </select>
           </div>
           </div>
           <div class="row">
           <div class="col-6">
            <div class="form-group">
      <label for="name">Name:</label>
      <input type="text" class="form-control" id="name" name="name" >
       </div>
       </div>
              <div class="form-group">
      <label for="name">GPN:</label>
      <input type="text" class="form-control" id="name" name="name">
       </div>
       </div>
       <div class="row">
           <div class="col-6">
            Filter State:
            <select class="custom-select" id="fil">
                <option value="">ALL</option>
                <option value=""></option>
                <option value=""></option>
            </select>
        </div>
         <button type="submit" class="btn btn-info" name="userSearch" >Search</button>
        </div><br>
        <h6 class="text-center">Registrations</h6>
        
        <div class="modal-body">
							
        <table id="dtVerticalScroll" class="table  table-hover table-striped table-bordered table-sm">
				<thead class="thead-light">
					<tr>
						<!-- <th class="th-sm">Event<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th> -->
						<th class="th-sm">GPN<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Name<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Status<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Phone<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Mail<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
						<th class="th-sm">Date<i class="fa fa-sort float-right"
							aria-hidden="true"></i>
						</th>
					</tr>
				</thead>
				<tbody>
					<c:forEach items="${categories}" var="cate" varStatus="status">
						<tr>
							<td>${categ.titel}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
							<td>${area.mandantName}</td>
						</tr>
					</c:forEach>
				</tbody>
			</table>
        </div>
        
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Excel Export</button>
        </div>
        
      </div>
    </div>
  </div>
  
 <!--  <script>
  function RegisterSearchBox(){
	  
	  var eventList = document.getElementsByClassName('custom-select');
	  /* var titel=document.getElementsByClassName('titelClass');
	  var active= document.getElementsByClassName('activeState');
	  var rBox="";*/
	  var inputBox=""; 
	alert( eventList.length);
	  
	  for(var i = 0; i < eventList.length; i++){
	      if(eventList[i].selectedIndex){
	    	   inputBox = $('#event').find('option:selected').text(); 
	          alert(inputBox);
	          
	          
	       
	      }
	    
	  } 
	  
	  
	  
  } 
  </script> -->
  
  
  
  
  <script type="text/javascript">
		$(function() {
			/*  Submit form using Ajax */
			$("button[name='userSearch']")
					.click(
							function(e) {

								//Prevent default submission of form
								e.preventDefault();

								//Remove all errors
								$('input').next().remove();
								
								 

								$
										.post({
											url : 'EventRegistrationDetail',
										 data : $('form[name=ucm]')
													.serialize(),  
													/* data: JSON.stringify({ selectedItems: $('#event').data('ListBox').dataItems() }), */		
											success : function(res) {
												inputBox = $('#event').find('option:selected').text(); 
												alert("pr");
												alert(JSON.stringify(res));
											}

										})
							});

		});
	</script>
  
  
  <!--  Registration Modal -->
  
  <!-- URL Modal -->
  
  
	
	<script  type="text/javascript">
   $(document).ready(function(){
	   $(".btn-show-value").click(function(){
		   var radioValue= $("input[name='idrow']:checked").val();
		   var radioValue_e= $("input[name='idrow']:checked").val();
		   var radioValue_f= $("input[name='idrow']:checked").val();
		   var radioValue_i= $("input[name='idrow']:checked").val();
		   var currLoc= window.location.origin;
		   
		  
		  
		   
	   
	   if(radioValue){
		  
		   document.getElementById("radio-value_d").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue+"&lang=d";
		   
			   document.getElementById("radio-value_e").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue_e+"&lang=e";
		   
			   document.getElementById("radio-value_f").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue_f+"&lang=f";
		   
			   document.getElementById("radio-value_i").value= currLoc+"/EventsAnmeldung.jsp?idrow="+radioValue_i+"&lang=i";
		   
		   
	   }
	   
   
   });
	   });
   
		  </script> 
		  
	  
   
  
  <div class="modal fade" id="urlModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        <!-- Modal Header -->
        <div class="modal-header">
          <h4 class="modal-title">URL</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
        <!-- Modal body -->
        
        <div class="modal-body">
        
        <script language="JavaScript">	
		function preview(lang){
		  var id = radioValue;
		  window.open("/RegisterLoginFormAction.do?idrow=" + id + "&lang=" + lang, "fenster", "height=850, width=900, status=1, location=no, scrollbars=1");
		}
	</script>
        
           <table border="0" cellpadding='0' cellspacing='0' width="100%"> 
           <tr>
           <td width="50" height="30">
           <a href="javascript:preview('d');" style="text-decoration: none">
			    <img src="<c:url value="/static/de.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400">
			<script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_d" size="80" readonly></p>
          </td>
          </tr>
          <tr>
			<td height="30">
			  <a href="javascript:preview('e');" style="text-decoration: none">
			    <img src="<c:url value="/static/en.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_e" size="80" readonly></p>
          </td></tr>
         <tr>
			<td height="30">
			  <a href="javascript:preview('f');" style="text-decoration: none">
			    <img src="<c:url value="/static/fr.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_f" size="80" readonly></p>
          </td></tr><tr>
			<td height="30">
			  <a href="javascript:preview('i');" style="text-decoration: none">
			    <img src="<c:url value="/static/it.gif" />"  border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script>
          <input type="text" id="radio-value_i" size="80" readonly></p>
          </td></tr>
           <tr> 
			<td colspan="3" align="left">
				<img src="<c:url value="/static/info_mouseover.gif" />"  border="0" style="vertical-align: top">&nbsp;
				Click on the flag in order to register a user.
			</td>
		</tr>
	</table> 
           
		<%-- <tr>
			<td width="50" height="30">
			  <a href="javascript:preview('d');" style="text-decoration: none">
			    <img src='static/de.gif' border="0" width="25" height="16" style="vertical-align: bottom">
			  </a>
			</td>
			<td width="5">&nbsp;</td>
			<td width="400"><script type="text/javascript" src=""></script><input name="url_de" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_de%>" size="100"  /></td>
		</tr>
		<tr>
			<td height="30">
			  <a href="javascript:preview('e');" style="text-decoration: none">
			    <img src='static/en.gif' border="0" width="25" height="16" style="vertical-align: bottom">
			  </a> 
			</td>
			<td>&nbsp;</td>
			<td><input name="url_en" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_en%>" size="100"></td>
		</tr>
		<tr>
			<td height="30">
				<a href="javascript:preview('f');" style="text-decoration: none">
				  <img src='static/fr.gif' border="0" width="25" height="16" style="vertical-align: bottom">
				</a> 			
			</td>
		  <td>&nbsp;</td>
			<td><input name="url_fr" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_fr%>" size="100"></td>
		</tr>
		<tr>
			<td height="30">
				<a href="javascript:preview('i');" style="text-decoration: none">
				  <img src='static//it.gif' border="0" width="25" height="16" style="vertical-align: bottom">
				</a>			
			</td>
			<td>&nbsp;</td>
			<td><input name="url_it" type="text" class="cuiEntryfieldReadOnly" readonly="readonly" value="<%=url_it%>" size="100"></td>
		</tr>
		<tr>
			<td colspan="3" height="10"></td>
		</tr> --%>
		<!-- <tr> 
			<td colspan="3" align="left">
				<img src='static/info_mouseover.gif' border="0" style="vertical-align: top">&nbsp;
				Click on the flag in order to register a user.

			</td>
		</tr>
	</table> -->
        </div>

        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Close</button>
        </div>
        
      </div>
    </div>
  </div>
  <!-- URL Modal -->
  
  <!-- New Modal -->
  <div class="modal fade" id="newModal">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
      
        
        <div class="modal-header">
          <h4 class="modal-title">Category Properties</h4>
          <button type="button" class="close" data-dismiss="modal">&times;</button>
        </div>
        
       
        <div class="modal-body">
         <form action="/action_page.php">
    <div class="form-group">
      <label for="name">Name Of Category:</label>
      <input type="text" class="form-control" id="name" name="name">
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio1">Activation State:
        <input type="radio" class="form-check-input" id="radio1" name="optradio" checked>On
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio2">
        <input type="radio" class="form-check-input" id="radio2" name="optradio">Off
      </label>
    </div><br><br>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio3">Visible In The List:
        <input type="radio" class="form-check-input" id="radio3" name="optradio1" checked>Visible
      </label>
    </div>
    <div class="form-check-inline">
      <label class="form-check-label" for="radio4">
        <input type="radio" class="form-check-input" id="radio4" name="optradio1">Not Visible
      </label>
    </div><br>
  </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn" data-dismiss="modal">Save</button>
        </div>
      </div>
    </div>
  </div>
  <!-- New Modal -->
  </div>
	</form:form>
</body>
<script type="text/javascript">
		var count = 0;
		$(function() {
			/*  Submit form using Ajax */
			$("button[name='categPermButton']")
					.click(
							function(e) {
alert("hi");
								//Prevent default submission of form
								e.preventDefault();

								//Remove all errors
								$('input').next().remove();

								$
										.post({
											url : 'permissions',
											data : $('form[name=ucm]')
													.serialize(),
											success : function(res) {

								alert(JSON.stringify(res));
											}
										})
							});

		});
	</script>
	
	<script type="text/javascript">
		var count = 0;
		$(function() {
			/*  Submit form using Ajax */
			$("button[name='regButton']")
					.click(
							function(e) {

								//Prevent default submission of form
								e.preventDefault();

								//Remove all errors
									$("#event").empty()

								$
										.post({
											url : 'registration',
											data : $('form[name=ucm]')
													.serialize(),
													success: function(res){
														alert(res.length);
														var dataLen = res.length;
														$('#event').append('<option value="">ALL</option>'); 
														for (i=0; i<dataLen; i++) {
															
															$('#event').append('<option value="' + res[i].event + '">' + res[i].event + '</option>'); 
														
														}
														alert(JSON.stringify(res));
														alert(res[0].eventidrow);
														
													}
													    })
													});
										});
						

		
	</script>
	
</html>












controller

package com.ubs.GAA.controller;

import java.util.List;

import javax.validation.Valid;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.MediaType;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.SessionAttributes;
import org.springframework.web.servlet.ModelAndView;

import com.ubs.GAA.model.EventModel;
import com.ubs.GAA.model.User;
import com.ubs.GAA.model.UserAreasModel;
import com.ubs.GAA.model.UserCategoriesModel;
import com.ubs.GAA.model.UserRoleModel;
import com.ubs.GAA.services.CategoryService;

@Controller
@RequestMapping("/categories")
@SessionAttributes(value = { "gpn", "userIdrow","areaId" })
public class CategoryPageController  {


	@Autowired
	private CategoryService categoryService;
	
	
	
	@RequestMapping(value="/")

	public ModelAndView CategoryPage(@ModelAttribute("gpn") String gpn, Model model, @ModelAttribute UserAreasModel uam,@ModelAttribute("areaId") Long areaId){

		
		List<UserCategoriesModel> categories = categoryService.ActiveUserCategories(gpn,areaId);
		model.addAttribute("categories", categories);
		model.addAttribute("ucm",new UserCategoriesModel());
		ModelAndView modl=new ModelAndView("categories");
		System.out.println(categories);

		return modl;
		
	}
	
	
	@RequestMapping(value="/save/")
	public String updateCategories(@ModelAttribute("idrow") Long idrow,@ModelAttribute UserCategoriesModel ucm,Model model){
		
		Long catIdrow=ucm.getIdrow();
		String titel=ucm.getTitel();
		Long code = ucm.getCode();
		
		
		Boolean catval= categoryService.updateCategory(titel,catIdrow,idrow,code);
		if(catval)
		{
			return "redirect:/categories/";
		}
		return "redirect:/GAA_Events/categories/";
		
	}
	
	@RequestMapping(value="/cd/")
	public String categoryDelete(@ModelAttribute("idrow") Long idrow,@ModelAttribute UserCategoriesModel ucm,Model model) {

		Long IDrow= ucm.getIdrow();
		Boolean value = categoryService.deleteCategory(IDrow);
		
		if (value) {
			
			return "redirect:/categories/";
		} else {
			model.addAttribute("msg", "Failed to delete the area");
			return "redirect:/Area/";
		}

	}
	
	/*@RequestMapping(value = "/permissions",produces = {MediaType.APPLICATION_JSON_VALUE})
	public @ResponseBody List<UserRole> getCategoryOwners(@ModelAttribute @Valid UserCategoriesModel ucm,Model model,BindingResult results){
		if(results.hasErrors()){
			return null;
		}else{
			Long categoryId=ucm.getIdrow();
			List<UserRole> list=categoryService.getCategoryOwners(categoryId);
			return list;
		}
	}
	
	@RequestMapping(value = "/deleteCategoryOwner",produces ={MediaType.APPLICATION_JSON_VALUE})
	public @ResponseBody String deleteCategoryOwner(@ModelAttribute UserCategoriesModel ucm, Model model,
			@ModelAttribute("idrow") Long idrow){
		
		Long categoryOwnerId=ucm.getOwnerId();
		String result;
		try{
			result=categoryService.deleteCategoryOwner(categoryOwnerId);
			return result;
		}catch (Exception e) {
			
			e.printStackTrace();
			return null;
		}
	}*/
	
	@RequestMapping(value = "/addCategoryOwner", produces ={MediaType.APPLICATION_JSON_VALUE})
	public @ResponseBody String addCategoryOwner(@ModelAttribute UserCategoriesModel ucm, Model model,
			@ModelAttribute("idrow") Long idrow){
		Long categoryId=ucm.getIdrow();
		String gpn=ucm.getGpn();
		
		
		
		
		return null;
		
	}
	
	@RequestMapping(value = "/registration",produces = {MediaType.APPLICATION_JSON_VALUE})
	public @ResponseBody List<UserCategoriesModel> EventList(@ModelAttribute @Valid  UserCategoriesModel ucm,Model model,BindingResult results){
		
 		Long categId=ucm.getIdrow();
		List<UserCategoriesModel> list = null;
		try {
			list = categoryService.EventList(categId);
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		
		return list;
		
	}
	
	@RequestMapping(value = "/EventRegistrationDetail",produces = {MediaType.APPLICATION_JSON_VALUE})
	public @ResponseBody List<UserCategoriesModel> EventRegistrationList(@ModelAttribute @Valid  UserCategoriesModel ucm,Model model,BindingResult results,@ModelAttribute @Valid  EventModel evm){
		
 		
 		Long eventId= ucm.getIdrow();
		List<UserCategoriesModel> list = null;
		try {
			list = categoryService.EventRegistrationList(eventId);
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		
		return list;
		
	}
	
	
}





service


package com.ubs.GAA.services;

import java.util.List;

import com.ubs.GAA.model.UserAreasModel;
import com.ubs.GAA.model.UserCategories;
import com.ubs.GAA.model.UserCategoriesModel;
import com.ubs.GAA.model.UserRole;


public interface CategoryService {
	

	
	List<UserCategoriesModel> ActiveUserCategories (String gpn, Long areaId) ;
	
	Boolean updateCategory(String titel, Long catIdrow,Long idrow,Long code);
	
	Boolean deleteCategory(Long idrow);

	String deleteCategoryOwner(Long categoryOwnerId) throws Exception;

	String insertCategoryOwner(Long categoryId, String gpn);

	List<UserRole> getCategoryOwners(Long categoryId);

	List<UserCategoriesModel> EventList(Long categId) throws Exception;
	
	List<UserCategoriesModel> EventRegistrationList(Long eventId) throws Exception;
	
	
	
	

}



Service Implementation

package com.ubs.GAA.services.servicesImpl;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import com.ubs.GAA.dao.CategoryDao;
import com.ubs.GAA.model.Event;
import com.ubs.GAA.model.Registration;
import com.ubs.GAA.model.UserAreas;
import com.ubs.GAA.model.UserAreasModel;
import com.ubs.GAA.model.UserCategories;
import com.ubs.GAA.model.UserCategoriesModel;
import com.ubs.GAA.model.UserRole;
import com.ubs.GAA.model.UserRoleModel;
import com.ubs.GAA.services.CategoryService;

@Service("CategoryService")
@Transactional
public class CategoryServiceImpl implements CategoryService {
	
	@Autowired
	private CategoryDao catdao;
	private UserCategoriesModel UserCategoriesModel;
	
	@SuppressWarnings("unused")
	@Override
	 public	List<UserCategoriesModel> ActiveUserCategories (String gpn,Long areaId) {
	 
	 
	 List<UserCategories> list = catdao.ActiveUserCategories(gpn,areaId);
	 List<UserCategoriesModel> catList = new ArrayList<UserCategoriesModel>();
	 for (int i=0;i<list.size();i++){
		 String titel=list.get(i).getTitel();
		 Long idrow= list.get(i).getIdrow();
		 Long idrowTblmandanten = list.get(i).getIdrowTblmandanten();
		 Long anzEvents = list.get(i).getAnzEvents();
		 Long recStatus = list.get(i).getRecStatus();
		 Long code = list.get(i).getCode();
		 String activeState;
		 String CUG;
	
		 if(list.get(i).getActiveState()==1l & list.get(i).getRecStatus()== 1l ){
			 activeState="yes";
			 CUG = "no";
			 UserCategoriesModel categ=new UserCategoriesModel(idrow, idrowTblmandanten, titel,activeState,CUG,anzEvents,recStatus,code);
			 catList.add(categ);
		}else{
			activeState=null;
		}
		 
		}
	 return catList;
	 
 }
 

 @Override
	public Boolean updateCategory(String titel,Long catIdrow,Long idrow,Long code)  {
	
	 return catdao.updateCategory(titel,catIdrow,idrow,code);
 }


@Override
public Boolean deleteCategory( Long idrow) {
	
	return catdao.deleteCategory( idrow);
}

@Override
public List<UserRole> getCategoryOwners(Long categoryId) {
	
	List<UserRole> list=catdao.getCategoryOwners(categoryId);
	/*List<UserCategoryModel> modelList=new ArrayList<UserCategoryModel>();
	for (int i=0;i<list.size();i++){
	
		Long idrow=list.get(i).getIdrow();
		String gpn=list.get(i).getGpn();
		UserCategoryModel uRolemodel=new UserCategoryModel(idrow,gpn);
	modelList.add(uRolemodel);
	}*/
	return list;
}


@Override
public String insertCategoryOwner(Long categoryId, String gpn) {
	
	try{	
		int result=catdao.insertCategoryOwner(categoryId, gpn);
		if (result==1){
			return "success";
		}else{
		return "failed";
		}
	}catch (Exception e) {
		return "failed";
	}
	}


@Override
public String deleteCategoryOwner(Long categoryOwnerId) throws Exception {
	
	try{
		int result = catdao.deleteCategoryOwner(categoryOwnerId);
		if (result==1){
			return "success";
		}else{
		return "failed";
		}
	}catch (Exception e) {
			return "failed";
	}
		
}


public List<UserCategoriesModel> EventList(Long categId) throws Exception {
	List<Event> list= catdao.EventList(categId);
	List<UserCategoriesModel> catList=new ArrayList<UserCategoriesModel>();
	for (int i=0;i<list.size();i++){
		String event=list.get(i).getTitel();
		Long eventidrow= list.get(i).getIdrow();
		UserCategoriesModel eventList=new UserCategoriesModel(event,eventidrow);
		catList.add(eventList);
	}
	
	
	return catList;
}

public List<UserCategoriesModel> EventRegistrationList(Long eventId) throws Exception {
	List<Registration> list= catdao.EventRegistrationList(eventId);
	List<UserCategoriesModel> catList=new ArrayList<UserCategoriesModel>();
	for (int i=0;i<list.size();i++){
		String gpn=list.get(i).getPersonalnummer();
		String firstName=list.get(i).getVorname();
		String lastName= list.get(i).getNachname();
		Long status= list.get(i).getRegisterStatus();
		String phone= list.get(i).getTelephoneinternal();
		String mail = list.get(i).getEmail();
		Date date= list.get(i).getRecCreatedate();
		String fullName= lastName + firstName;
		UserCategoriesModel eventRegisterList=new UserCategoriesModel(gpn,fullName,status,phone,mail,date);
		catList.add(eventRegisterList);
	}
	
	
	return catList;
}





}





DAOIMPLementation


package com.ubs.GAA.dao.daoImpl;

import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.List;

import org.hibernate.Criteria;
import org.hibernate.criterion.Restrictions;
import org.hibernate.jdbc.Work;
import org.springframework.stereotype.Repository;
import org.springframework.transaction.annotation.Transactional;

import com.ubs.GAA.dao.AbstractDao;
import com.ubs.GAA.dao.CategoryDao;
import com.ubs.GAA.model.Area;
import com.ubs.GAA.model.Category;
import com.ubs.GAA.model.EnhancedEvent;
import com.ubs.GAA.model.Event;
import com.ubs.GAA.model.Registration;
import com.ubs.GAA.model.UserAreas;
import com.ubs.GAA.model.UserCategories;
import com.ubs.GAA.model.UserRole;

import oracle.jdbc.OracleTypes;

@Repository("CategoryDao")
public class CategoryDaoImpl extends AbstractDao<Integer> implements CategoryDao {
	
	protected int output;
	protected int delOutput;

	@Override
	@Transactional
	public List<UserCategories> ActiveUserCategories (String gpn,Long areaId){
		
		
		Criteria crit=createEntityCriteria(UserCategories.class);
		crit.add(Restrictions.eq("gpn",gpn));
		crit.add(Restrictions.eq("idrowTblmandanten",areaId));
		crit.add(Restrictions.eq("recStatus",1l));
		List<UserCategories> results=crit.list();
		
		return results;
	}

	
	@Override
	public Boolean deleteCategory(Long idrow) {
		// TODO Auto-generated method stub
		try{
			Criteria crit=createEntityCriteria(Category.class);
			crit.add(Restrictions.eq("idrow", idrow));
			Category categ = (Category) crit.uniqueResult();
			categ.setRecStatus(0l);
			categ.setModifiedBy(idrow);
			persist(categ);
			return true;
			}catch (Exception e) {
				return false;
			}
		
	}
		
	

	@Override
	public Boolean updateCategory(String titel, Long catIdrow,Long idrow,Long code) {
		try{
			Criteria crit= createEntityCriteria(Category.class);
			crit.add(Restrictions.eq("idrow",catIdrow));
			Category categ = (Category) crit.uniqueResult();
			categ.setTitel(titel);
			categ.setCode(code);
			categ.setModifiedBy(idrow);
			persist(categ);
			
			return true;
		}catch (Exception e) {
			return false;
		}
		
	}
	
	@SuppressWarnings("unchecked")
	@Override
	@Transactional
	public List<UserRole> getCategoryOwners(Long categoryId) {
		try{
			Criteria crit=createEntityCriteria(UserRole.class);
			crit.add(Restrictions.eq("rolle", 11));
			crit.add(Restrictions.eq("idrowTblmandant", categoryId));
			crit.add(Restrictions.eq("recStatus", 1L));
			List<UserRole> list=crit.list();
			//List<UserCategories> results=crit.list();
			return list;
		}catch(Exception e){
			return null;
		}
	}

	@Override
	public int insertCategoryOwner(Long categoryId, String gpn) {	
		try{
			
			getSession().doWork(new Work() {
				
				@Override
				public void execute(Connection connection) throws SQLException {
					CallableStatement call = connection.prepareCall("{ ? = call GAA_PG_AUTHORISATION.insert_categoryOwner(?,?) }");
				    call.registerOutParameter( 1, OracleTypes.INTEGER ); 
				    call.setLong(2,categoryId);
				    call.setString(3, gpn);
				    call.execute();
					output=call.getInt(1);
				}
			});
			return output; 
		}catch(Exception e){
			return output;
		}
	}

	@Override
	@Transactional
	public int deleteCategoryOwner(Long categoryOwnerId) throws Exception {
		try{
			
			getSession().doWork(new Work() {
				
				@Override
				public void execute(Connection connection) throws SQLException {
					// TODO Auto-generated method stub
					CallableStatement call = connection.prepareCall(" {? = call GAA_PG_AUTHORISATION.delete_categoryOwner(?)}");
				    call.registerOutParameter( 1, OracleTypes.INTEGER );
				    call.setLong(2, categoryOwnerId);
				    call.execute();
				     delOutput = call.getInt(1);
					
				}
			});

				
			
			return delOutput;
		}catch (Exception e) {
			e.printStackTrace();
			return delOutput;
		}
	}


	public List<Event> EventList(Long categId) throws Exception {
 
		try{
		Criteria crit=createEntityCriteria(Event.class);
		crit.add(Restrictions.eq("idrowTblevents",categId));
		crit.add(Restrictions.eq("recStatus", 1L));
		List<Event> results=crit.list();
		return results;
		
	}catch(Exception e){
		return null;
	}

	}
	
	public List<Registration> EventRegistrationList(Long eventId) throws Exception {
		 
		try{
		Criteria crit=createEntityCriteria(Registration.class);
		crit.add(Restrictions.eq("IDROW_TBLEVENTS_ITEMS",eventId));
		crit.add(Restrictions.eq("recStatus", 1L));
		List<Registration> results=crit.list();
		return results;
		
	}catch(Exception e){
		return null;
	}

	}
	
}
	
	




DAO

package com.ubs.GAA.dao;

import java.util.List;

import com.ubs.GAA.model.Event;
import com.ubs.GAA.model.Registration;
import com.ubs.GAA.model.UserCategories;
import com.ubs.GAA.model.UserRole;

public interface CategoryDao {

	Boolean deleteCategory(Long idrow);

	List<UserCategories> ActiveUserCategories(String gpn, Long areaId);

	Boolean updateCategory(String titel, Long catIdrow, Long idrow, Long code);

	List<UserRole> getCategoryOwners(Long categoryId);

	int insertCategoryOwner(Long categoryId, String gpn);

	int deleteCategoryOwner(Long categoryOwnerId) throws Exception;

	List<Event> EventList(Long categId) throws Exception;
	
	List<Registration> EventRegistrationList(Long eventId) throws Exception;
	
	
	
}




MODEL

package com.ubs.GAA.model;

import java.util.Date;
import java.util.List;

public class UserCategoriesModel {
	private Long categId;
	public Long getCategId() {
		return categId;
	}
	public void setCategId(Long categId) {
		this.categId = categId;
	}
	
	private String event;
	
	
	public String getEvent() {
		return event;
	}
	public void setEvent(String event) {
		this.event = event;
	}

	private Long eventidrow;
	


	public Long getEventidrow() {
		return eventidrow;
	}
	public void setEventidrow(Long eventidrow) {
		this.eventidrow = eventidrow;
	}

	private Long idrow;
	private Long idrowTblmandanten;
	private String titel;
	private String gpn;
	private Long userRole;
	private Long code;
	private String activeState;
	private String hasClosedUserGroup;
	private Long sortOrder;
	private Long anzEvents;
	private Long createdBy;
	private Long modifiedBy;
	private Date recCreatedate;
	private Date recModifydate;
	private Long recStatus;
	private String fullName;
	private Long status;
	private String phone;
	private String mail;
	private Date date;
	
	public String getFullName() {
		return fullName;
	}
	public void setFullName(String fullName) {
		this.fullName = fullName;
	}
	public Long getStatus() {
		return status;
	}
	public void setStatus(Long status) {
		this.status = status;
	}
	public String getPhone() {
		return phone;
	}
	public void setPhone(String phone) {
		this.phone = phone;
	}
	public String getMail() {
		return mail;
	}
	public void setMail(String mail) {
		this.mail = mail;
	}
	public Date getDate() {
		return date;
	}
	public void setDate(Date date) {
		this.date = date;
	}

	private List <UserCategoriesModel> catlist;
	public UserCategoriesModel() {
		
	}
	public UserCategoriesModel(Long idrow,Long idrowTblmandanten,String titel,String activeState,String hasClosedUserGroup,Long anzEvents,Long recStatus,Long code){
		this.idrow=idrow;
		this.idrowTblmandanten=idrowTblmandanten;
		this.titel=titel;
		this.activeState= activeState;
		this.hasClosedUserGroup= hasClosedUserGroup;
		this.anzEvents=  anzEvents;
		this.recStatus= recStatus;
		this.code = code;
	}
	public UserCategoriesModel(String event, Long eventidrow) {
		// TODO Auto-generated constructor stub
		this.event= event;
		this.eventidrow= eventidrow;
	}
	
	public UserCategoriesModel(String gpn,String fullName,Long status,String phone,String mail,Date date){
		this.gpn= gpn;
		this.fullName= fullName;
		this.status= status;
		this.phone= phone;
		this.mail= mail;
		this.date=date;
	}
	
	public Long getIdrow() {
		return idrow;
	}
	public void setIdrow(Long idrow) {
		this.idrow = idrow;
	}
	public Long getIdrowTblmandanten() {
		return idrowTblmandanten;
	}
	public void setIdrowTblmandanten(Long idrowTblmandanten) {
		this.idrowTblmandanten = idrowTblmandanten;
	}
	public String getTitel() {
		return titel;
	}
	public void setTitel(String titel) {
		this.titel = titel;
	}
	public String getGpn() {
		return gpn;
	}
	public void setGpn(String gpn) {
		this.gpn = gpn;
	}
	public Long getUserRole() {
		return userRole;
	}
	public void setUserRole(Long userRole) {
		this.userRole = userRole;
	}
	public Long getCode() {
		return code;
	}
	public void setCode(Long code) {
		this.code = code;
	}
	public String getActiveState() {
		return activeState;
	}
	public void setActiveState(String activeState) {
		this.activeState = activeState;
	}
	public String getHasClosedUserGroup() {
		return hasClosedUserGroup;
	}
	public void setHasClosedUserGroup(String hasClosedUserGroup) {
		this.hasClosedUserGroup = hasClosedUserGroup;
	}
	public Long getSortOrder() {
		return sortOrder;
	}
	public void setSortOrder(Long sortOrder) {
		this.sortOrder = sortOrder;
	}
	public Long getAnzEvents() {
		return anzEvents;
	}
	public void setAnzEvents(Long anzEvents) {
		this.anzEvents = anzEvents;
	}
	public Long getCreatedBy() {
		return createdBy;
	}
	public void setCreatedBy(Long createdBy) {
		this.createdBy = createdBy;
	}
	public Long getModifiedBy() {
		return modifiedBy;
	}
	public void setModifiedBy(Long modifiedBy) {
		this.modifiedBy = modifiedBy;
	}
	public Date getRecCreatedate() {
		return recCreatedate;
	}
	public void setRecCreatedate(Date recCreatedate) {
		this.recCreatedate = recCreatedate;
	}
	public Date getRecModifydate() {
		return recModifydate;
	}
	public void setRecModifydate(Date recModifydate) {
		this.recModifydate = recModifydate;
	}
	public Long getRecStatus() {
		return recStatus;
	}
	public void setRecStatus(Long recStatus) {
		this.recStatus = recStatus;
	}
	public List<UserCategoriesModel> getCatlist() {
		return catlist;
	}
	public void setCatlist(List<UserCategoriesModel> catlist) {
		this.catlist = catlist;
	}
	
	
	

}
