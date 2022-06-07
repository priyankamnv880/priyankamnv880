using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
  
namespace CRUDDemo.Controllers
{
    public class CRUDController : Controller
    {
        // To create View of this Action result
        public ActionResult create() 
        {
            return View();
        }
  
        // Specify the type of attribute i.e.
        // it will add the record to the database
        [HttpPost] 
        public ActionResult create(Spotify model)
        {
              
            // To open a connection to the database
            using(var context = new demoCRUDEntities()) 
            {
                // Add data to the particular table
                context.Spotify.Add(model); 
                  
                // save the changes
                context.SaveChanges(); 
            }
            string message = "Created the record successfully";
              
            // To display the message on the screen
            // after the record is created successfully
            ViewBag.Message = message;     
              
            // write @Viewbag.Message in the created
            // view at the place where you want to
            // display the message
            return View(); 
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
  
namespace CRUDDemo.Controllers
{
    public class CRUDController : Controller {
        [HttpGet] // Set the attribute to Read
            public ActionResult
            Read()
        {
            using(var context = new demoCRUDEntities())
            {
                  
                // Return the list of data from the database
                var data = context.Spotify.ToList(); 
                return View(data);
            }
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
  
namespace CRUDDemo.Controllers
{
    public class CRUDController : Controller
    {
          
        // To fill data in the form 
        // to enable easy editing
        public ActionResult Update(int Spotifyid) 
        {
            using(var context = new demoCRUDEntities())
            {
                var data = context.Spotify.Where(x => x.SpotifyNo == Spotifyid).SingleOrDefault();
                return View(data);
            }
        }
  
        // To specify that this will be 
        // invoked when post method is called
        [HttpPost]
        [ValidateAntiForgeryToken] 
        public ActionResult Update(int Spotifyid, Spotify model)
        {
            using(var context = new demoCRUDEntities())
            {
                  
                // Use of lambda expression to access
                // particular record from a database
                var data = context.Spotify.FirstOrDefault(x => x.SpotifyNo == Spotifyid); 
                  
                // Checking if any such record exist 
                if (data != null) 
                {
                    artistdata.Name = model.Name;
                    artistdata.DOB = model.DOB;
                    artistdata.Bio = model.Bio;
                    Songdata.Name = model.Name;
                    Songdata.Date of Release = model.Date of Release;
                    Songdata.Cover = model.Cover;
                    Userdata.Name = model.Name;
                    Userdata.EmailId = model.EmailId;
                    context.SaveChanges();
                      
                    // It will redirect to 
                    // the Read method
                    return RedirectToAction("Read"); 
                }
                else
                    return View();
            }
        }
    }
}
